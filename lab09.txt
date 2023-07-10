/*1. Crie um programa que:
a) Aloque dinamicamente um array de 5 números inteiros;
b) Peça para o usuário digitar os 5 números no espaço alocado;
c) Mostre na tela os 5 números;
d) Libere a memória alocada*/

#include <stdio.h>
#include <stdlib.h>

int main(){
    int *ptr, i;
    /*alocando espaço para 5 inteiros*/
    ptr = (int*)malloc(5 * sizeof(int));

    /*armazeando os 5 inteiros no espaço alocado*/
    for(i = 0 ; i < 5; i++){
        printf("Entre com n[%d]: ", i+1);
        scanf("%d", &ptr[i]);
    }
    /*mostrando os 5 inteiros*/
    for(i = 0 ; i < 5; i++){
        printf("%d  ", ptr[i]);
    }
    /*desalocando o espaço utilizado anteriormente*/
    free(ptr);
    return 0;
}
------------------------------------------------------
/* 2. Faça um programa que leia do usuário o tamanho de um vetor a ser lido
e faça a alocação dinâmica de memória. Em seguida, leia do usuário
seus valores e imprima o vetor lido.*/

#include <stdio.h>
#include <stdlib.h>

int main() {

    int tamanho;
    int* vetor;  

    printf("Digite o tamanho do vetor: ");
    scanf("%d", &tamanho);
// Alocação dinâmica de memória para o vetor
    vetor = (int*) malloc(tamanho * sizeof(int));
    
    if (vetor == NULL) {
        
        printf("Erro na alocação de memória.\n");
        return 1;
    }

// Leitura dos valores do vetor
    for (int i = 0; i < tamanho; i++) {
        printf("Digite o valor para o elemento %d: ", i + 1);
        scanf("%d", &vetor[i]);
    }

// Impressão do vetor  
printf("Vetor lido:\n");
    for (int i = 0; i < tamanho; i++) {       
        printf("%d ", vetor[i]);
    } 

printf("\n");
// Liberação da memória alocada
    free(vetor);

return 0;
}
------------------------------------------------------
/* 3. Faça um programa que leia do usuário o tamanho de um vetor a ser lido
e faça a alocação dinâmica de memória. Em seguida, leia do usuário
seus valores e mostre quantos dos números são pares e quantos são
ímpares.*/

#include <stdio.h>
#include <stdlib.h>

int main(){
    int i, n;
    char *ptr;

    printf("Entre com o tamanho da string: ");
    scanf("%d", &n);

    /*alocando espaço para n inteiros*/
    ptr = (char*)malloc(n * sizeof(char));

    printf("Digite a string: ");
    scanf(" %[^\n]", ptr);
    i = 0;
    /*mostrando a string sem vogais*/
    while(ptr[i] != '\0'){
        if(ptr[i]!= 'a' && ptr[i]!= 'A' && ptr[i]!= 'e' && ptr[i]!= 'E' && ptr[i]!= 'i' && ptr[i]!= 'I' 
	&& ptr[i]!= 'o' && ptr[i]!= 'O' && ptr[i]!= 'u' && ptr[i]!= 'U')
            printf("%c  ", ptr[i]);
            i++;
    }
    /*desalocando o espaço utilizado anteriormente*/
    free(ptr);
    return 0;
}
---------------------------------------------------------------------
/* 4. Faça um programa que receba do usuário o tamanho de uma string e
chame uma função para alocar dinamicamente essa string. Em seguida,
o usuário deverá informar o conteúdo dessa string. O programa imprime
a string sem suas vogais.*/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *removeVowels(const char *str) {
    int length = strlen(str);
    char *result = (char *)malloc((length + 1) * sizeof(char)); // Aloca memória para a nova string
    int j = 0; // Índice para a nova string sem vogais

    for (int i = 0; i < length; i++) {
        char ch = str[i];

        // Verifica se o caractere atual não é uma vogal
        if (ch != 'a' && ch != 'e' && ch != 'i' && ch != 'o' && ch != 'u') {
            result[j] = str[i];
            j++;
        }
    }

    result[j] = '\0'; // Adiciona o caractere nulo de terminação da string

    return result;
}

int main() {
    int length;
    char *str;

    printf("Digite o tamanho da string: ");
    scanf("%d", &length);

    // Aloca memória dinamicamente para a string com base no tamanho informado
    str = (char *)malloc((length + 1) * sizeof(char));

    printf("Digite o conteudo da string: ");
    scanf(" %[^\n]s", str);

    // Remove as vogais da string
    char *result = removeVowels(str);

    printf("String sem vogais: %s\n", result);

    // Libera a memória alocada
    free(str);
    free(result);

    return 0;
}
---------------------------------------------------------------------
/* 5. Faça um programa que leia um número N e:
a) Crie dinamicamente e leia um vetor de inteiro de N posições;
b) Leia um número inteiro X e conte e mostre os múltiplos desse número
que existem no vetor.*/

#include <stdio.h>
#include <stdlib.h>

int countMultiples(int *vector, int size, int number) {
    int count = 0;

    for (int i = 0; i < size; i++) {
        if (vector[i] % number == 0) {
            count++;
        }
    }

    return count;
}

int main() {
    int n;
    printf("Digite o tamanho do vetor: ");
    scanf("%d", &n);

    int *vector = (int *)malloc(n * sizeof(int));

    printf("Digite os elementos do vetor:\n");
    for (int i = 0; i < n; i++) {
        scanf("%d", &vector[i]);
    }

    int x;
    printf("Digite um número inteiro: ");
    scanf("%d", &x);

    int multiples = countMultiples(vector, n, x);

    printf("Existem %d multiplos de %d no vetor.\n", multiples, x);

    free(vector);

    return 0;
}
---------------------------------------------------------------------
/* 6. Faça um programa que simule a memória de um computador: o usuário
irá especifcar o tamanho da memória, ou seja, quantos bytes serão
alocados do tipo inteiro. Para tanto, a memória solicitada deve ser um
valor múltiplo do tamanho do tipo inteiro. Em seguida, o usuário terá 2
opções: inserir um valor em uma determinada posição ou consultar o
valor contido em uma determinada posição. A memória deve iniciar com
todos os dados zerados.*/

#include <stdio.h>
#include <stdlib.h>

int main() {
    int memorySize;
    int *memory = NULL;

    printf("Digite o tamanho da memória (em bytes): ");
    scanf("%d", &memorySize);

    // Verifica se o tamanho da memória é um valor múltiplo do tamanho do tipo inteiro
    if (memorySize % sizeof(int) != 0) {
        printf("Tamanho da memória inválido.\n");
        return 0;
    }

    int numElements = memorySize / sizeof(int);

    // Aloca memória dinamicamente para o vetor de inteiros
    memory = (int *)malloc(memorySize);

    // Inicializa todos os elementos da memória com valor zero
    for (int i = 0; i < numElements; i++) {
        memory[i] = 0;
    }

    int option;
    do {
        printf("\nOpções:\n");
        printf("1. Inserir valor em uma posição\n");
        printf("2. Consultar valor em uma posição\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &option);

        switch (option) {
            case 1:
            {
                int position, value;
                printf("\nDigite a posição: ");
                scanf("%d", &position);
                printf("Digite o valor: ");
                scanf("%d", &value);

                if (position >= 0 && position < numElements) {
                    memory[position] = value;
                    printf("Valor inserido com sucesso.\n");
                } else {
                    printf("Posição inválida.\n");
                }

                break;
            }
            case 2:
            {
                int position;
                printf("\nDigite a posição: ");
                scanf("%d", &position);

                if (position >= 0 && position < numElements) {
                    int value = memory[position];
                    printf("Valor na posição %d: %d\n", position, value);
                } else {
                    printf("Posição inválida.\n");
                }

                break;
            }
            case 0:
                printf("\nEncerrando o programa.\n");
                break;
            default:
                printf("\nOpção inválida.\n");
                break;
        }

    } while (option != 0);

    free(memory);

    return 0;
}
---------------------------------------------------------------------
/* 7. Escreva um programa que leia primeiro os 6 números gerados pela
loteria e depois os 6 números do seu bilhete. O programa então compara
quantos números o jogador acertou. Em seguida, ele aloca espaço para
um vetor de tamanho igual a quantidade de números corretos e guarda
os números corretos nesse vetor. Finalmente, o programa exibe os
números sorteados e os seus números corretos.*/

#include <stdio.h>
#include <stdlib.h>

int main() {
    int lotteryNumbers[6];
    int playerNumbers[6];

    printf("Digite os 6 números sorteados pela loteria:\n");
    for (int i = 0; i < 6; i++) {
        scanf("%d", &lotteryNumbers[i]);
    }

    printf("Digite os 6 números do seu bilhete:\n");
    for (int i = 0; i < 6; i++) {
        scanf("%d", &playerNumbers[i]);
    }

    int count = 0; // Quantidade de números corretos
    int *correctNumbers = NULL; // Vetor para armazenar os números corretos

    // Verifica quantos números foram acertados
    for (int i = 0; i < 6; i++) {
        for (int j = 0; j < 6; j++) {
            if (playerNumbers[i] == lotteryNumbers[j]) {
                count++;
                break;
            }
        }
    }

    // Aloca espaço para o vetor de tamanho igual à quantidade de números corretos
    correctNumbers = (int *)malloc(count * sizeof(int));

    int index = 0;
    // Armazena os números corretos no vetor
    for (int i = 0; i < 6; i++) {
        for (int j = 0; j < 6; j++) {
            if (playerNumbers[i] == lotteryNumbers[j]) {
                correctNumbers[index] = playerNumbers[i];
                index++;
                break;
            }
        }
    }

    printf("\nNúmeros sorteados pela loteria: ");
    for (int i = 0; i < 6; i++) {
        printf("%d ", lotteryNumbers[i]);
    }

    printf("\nSeus números corretos: ");
    for (int i = 0; i < count; i++) {
        printf("%d ", correctNumbers[i]);
    }
    printf("\n");

    free(correctNumbers);

    return 0;
}
---------------------------------------------------------------------
/* 8. Faça um programa para armazenar em memória um vetor de dados
contendo 1500 valores do tipo int, usando a função de alocação
dinâmica de memória CALLOC:
a) Faça um loop e verifique se o vetor contém realmente os 1500
valores inicializados com zero (conte os 1500 zeros do vetor);
b) Atribua para cada elemento do vetor o valor do seu índice junto a
este vetor;
c) Exibir na tela os 10 primeiros e os 10 últimos elementos do vetor.*/

#include <stdio.h>
#include <stdlib.h>

int main(){
    int *ptr, i;
    /*alocando espaço para 1500 inteiros*/
    ptr = (int*)calloc(1500 , sizeof(int));
    /*atribuindo o valor do indice a cada espaço do vetpr alocado*/
    for(i = 0 ; i < 1500; i++){
       ptr[i] = i;
    }
     /*imprimindo os 10 primeiros e 10 ultimos numeros*/
    for(i = 0 ; i < 1500; i++){
       if(i <= 9 || i > 1489)
            printf("%d ", ptr[i]);
    }
    /*desalocando o espaço utilizado anteriormente*/
    free(ptr);
    return 0;
}
----------------------------------------------------------------------------------
/* 9. Faça um programa que leia uma quantidade qualquer de números
armazenando-os na memória e pare a leitura quando o usuário entrar
um número negativo. Em seguida, imprima o vetor lido. Use a função
REALLOC.*/

#include <stdio.h>
#include <stdlib.h>

int main() {
    int size = 1; // Tamanho inicial do vetor
    int count = 0; // Quantidade de números lidos
    int *numbers = (int *)malloc(size * sizeof(int)); // Vetor para armazenar os números

    if (numbers == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    int number;

    printf("Digite os números (digite um número negativo para parar):\n");

    while (1) {
        scanf("%d", &number);

        if (number < 0) {
            break;
        }

        if (count == size) {
            // Se o vetor estiver cheio, realoca o dobro do tamanho atual
            size *= 2;
            numbers = (int *)realloc(numbers, size * sizeof(int));

            if (numbers == NULL) {
                printf("Erro de realocação de memória.\n");
                return 1;
            }
        }

        numbers[count] = number;
        count++;
    }

    printf("\nNúmeros lidos:\n");
    for (int i = 0; i < count; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    free(numbers);

    return 0;
}
----------------------------------------------------------------------------------
/* 10.Faça um programa que pergunte ao usuário quantos valores ele deseja
armazenar em um vetor de double, depois use a função MALLOC para
reservar (alocar) o espaço de memória de acordo com o especifcado
pelo usuário. Esse vetor deve ter um tamanho maior ou igual a 10
elementos. Use este vetor dinâmico como um vetor comum, atribuindo
aos 10 primeiros elementos do vetor valores aleatórios (usando a função
rand) entre 0 e 100. Exiba na tela os valores armazenados nos 10
primeiros elementos do vetor.*/

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    int size;

    printf("Digite a quantidade de valores a serem armazenados (no mínimo 10): ");
    scanf("%d", &size);

    if (size < 10) {
        printf("Tamanho inválido. O vetor deve ter no mínimo 10 elementos.\n");
        return 1;
    }

    double *vector = (double *)malloc(size * sizeof(double));

    if (vector == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    srand(time(NULL));

    for (int i = 0; i < 10; i++) {
        vector[i] = (double)(rand() % 101);
    }

    printf("\nValores armazenados nos 10 primeiros elementos do vetor:\n");
    for (int i = 0; i < 10; i++) {
        printf("%.2lf ", vector[i]);
    }
    printf("\n");

    free(vector);

    return 0;
}
----------------------------------------------------------------------------------
/* 11.Crie um programa que declare uma estrutura (registro) para o cadastro
de alunos.
a) Deverão ser armazenados, para cada aluno: matrícula, sobrenome
(apenas um) e ano de nascimento;
b) Ao início do programa, o usuário deverá informar o número de alunos
que serão armazenados;
c) O programa deverá alocar dinamicamente a quantidade necessária
de memória para armazenar os registros dos alunos;
d) O programa deverá pedir ao usuário que entre com as informações
dos alunos.
e) Ao fnal, mostrar os dados armazenados e liberar a memória alocada.*/

#include <stdio.h>
#include <stdlib.h>

struct aluno{
    int matricula;
    char nome[40];
    int ano_nasc;
};
typedef struct aluno aluno;
int main(){
    int n, i;
    aluno *ptr;
    printf("Entre com o numero de registros a serem alocados: ");
    scanf("%d", &n);
    /*alocando espaço para n iregistros*/
    ptr = (aluno*)malloc(n * sizeof(aluno));

    /*armazeando os n registros no espaço alocado*/
    for(i = 0 ; i < n; i++){
        printf("Numero de matricula: ");
        scanf("%d", &ptr[i].matricula);
        printf("Nome: ");
        scanf(" %[^\n]", ptr[i].nome);
        printf("Ano de nascimento: ");
        scanf("%d", &ptr[i].ano_nasc);
        printf("\n\n");
    }
    /*mostrando os n registros armazenados*/
    for(i = 0 ; i < n; i++){
        printf("Numero de matricula %d \n", ptr[i].matricula);
        printf("Nome: %s \n" , ptr[i].nome);
        printf("Ano de nascimento: %d\n\n" , ptr[i].ano_nasc);
    }
    /*desalocando o espaço utilizado anteriormente*/
    free(ptr);
    return 0;
}
-----------------------------------------------------------------
/* 12.Considere um cadastro de produtos de um estoque, com as seguintes
informações para cada produto:
 Código de identifcação do produto: representado por um valor
inteiro
 Nome do produto: com até 50 caracteres
 Quantidade disponível no estoque: representado por um número
inteiro
 Preço de venda: representado por um valor real
a) Defna uma estrutura, denominada produto, que tenha os campos
apropriados para guardar as informações de um produto;
b) Crie um conjunto de N produtos (N é um valor fornecido pelo usuário)
e peca ao usuário para entrar com as informações de cada produto;
c) Encontre o produto com o maior preço de venda;
d) Encontre o produto com a maior quantidade disponível no estoque.*/

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definição da estrutura Produto
typedef struct {
    int codigo;
    char nome[50];
    int quantidade;
    float preco;
} Produto;

int main() {
    int N; // Quantidade de produtos
    int i;

    printf("Digite a quantidade de produtos: ");
    scanf("%d", &N);

    // Aloca espaço para o vetor de produtos
    Produto *produtos = (Produto *)malloc(N * sizeof(Produto));

    if (produtos == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    // Preenche as informações de cada produto
    for (i = 0; i < N; i++) {
        printf("\nProduto %d:\n", i + 1);

        printf("Codigo: ");
        scanf("%d", &(produtos[i].codigo));

        printf("Nome: ");
        scanf(" %[^\n]s", produtos[i].nome);

        printf("Quantidade: ");
        scanf("%d", &(produtos[i].quantidade));

        printf("Preco de venda: ");
        scanf("%f", &(produtos[i].preco));
    }

    // Encontra o produto com o maior preço de venda
    int maxPrecoIndex = 0;
    for (i = 1; i < N; i++) {
        if (produtos[i].preco > produtos[maxPrecoIndex].preco) {
            maxPrecoIndex = i;
        }
    }

    // Encontra o produto com a maior quantidade disponível no estoque
    int maxQuantidadeIndex = 0;
    for (i = 1; i < N; i++) {
        if (produtos[i].quantidade > produtos[maxQuantidadeIndex].quantidade) {
            maxQuantidadeIndex = i;
        }
    }

    // Exibe o produto com o maior preço de venda
    printf("\nProduto com o maior preco de venda:\n");
    printf("Ccdigo: %d\n", produtos[maxPrecoIndex].codigo);
    printf("Nome: %s\n", produtos[maxPrecoIndex].nome);
    printf("Quantidade: %d\n", produtos[maxPrecoIndex].quantidade);
    printf("Preco de venda: %.2f\n", produtos[maxPrecoIndex].preco);

    // Exibe o produto com a maior quantidade disponível no estoque
    printf("\nProduto com a maior quantidade disponivel no estoque:\n");
    printf("Codigo: %d\n", produtos[maxQuantidadeIndex].codigo);
    printf("Nome: %s\n", produtos[maxQuantidadeIndex].nome);
    printf("Quantidade: %d\n", produtos[maxQuantidadeIndex].quantidade);
    printf("Preco de venda: %.2f\n", produtos[maxQuantidadeIndex].preco);

    // Libera a memória alocada
    free(produtos);

    return 0;
}
-------------------------------------------------------------------------------------
/* 13.Escreva um programa que aloque dinamicamente uma matriz (de
inteiros) de dimensões defnidas pelo usuário e a leia. Em seguida,implemente uma função que receba um valor, retorne 1 caso o valor
esteja na matriz ou retorne 0 caso não esteja na matriz.*/

#include <stdio.h>
#include <stdlib.h>

int valorNaMatriz(int **matriz, int linhas, int colunas, int valor) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            if (matriz[i][j] == valor) {
                return 1; // Valor encontrado na matriz
            }
        }
    }

    return 0; // Valor não encontrado na matriz
}

int main() {
    int linhas, colunas;

    printf("Digite o número de linhas da matriz: ");
    scanf("%d", &linhas);

    printf("Digite o número de colunas da matriz: ");
    scanf("%d", &colunas);

    // Aloca espaço para a matriz
    int **matriz = (int **)malloc(linhas * sizeof(int *));
    if (matriz == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    for (int i = 0; i < linhas; i++) {
        matriz[i] = (int *)malloc(colunas * sizeof(int));
        if (matriz[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Preenche a matriz com os valores informados pelo usuário
    printf("Digite os valores da matriz:\n");
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            scanf("%d", &matriz[i][j]);
        }
    }

    int valor;

    printf("Digite um valor para buscar na matriz: ");
    scanf("%d", &valor);

    // Chama a função valorNaMatriz para verificar se o valor está presente
    int encontrado = valorNaMatriz(matriz, linhas, colunas, valor);

    if (encontrado) {
        printf("O valor %d está presente na matriz.\n", valor);
    } else {
        printf("O valor %d não está presente na matriz.\n", valor);
    }

    // Libera a memória alocada para a matriz
    for (int i = 0; i < linhas; i++) {
        free(matriz[i]);
    }
    free(matriz);

    return 0;
}
---------------------------------------------------------------------
/* 14.Construa um programa que leia o número de linhas e de colunas de uma
matriz de números reais, aloque espaço dinamicamente para esta e a
inicialize com valores fornecidos pelo usuário. Ao fnal, o programa
deverá retornar a matriz na saída padrão com layout apropriado.*/
#include <stdio.h>
#include <stdlib.h>

int main() {
    int linhas, colunas;

    printf("Digite o número de linhas da matriz: ");
    scanf("%d", &linhas);

    printf("Digite o número de colunas da matriz: ");
    scanf("%d", &colunas);

    // Aloca espaço para a matriz
    float **matriz = (float **)malloc(linhas * sizeof(float *));
    if (matriz == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    for (int i = 0; i < linhas; i++) {
        matriz[i] = (float *)malloc(colunas * sizeof(float));
        if (matriz[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Preenche a matriz com os valores informados pelo usuário
    printf("Digite os valores da matriz:\n");
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            scanf("%f", &matriz[i][j]);
        }
    }

    // Imprime a matriz com layout apropriado
    printf("\nMatriz:\n");
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            printf("%.2f ", matriz[i][j]);
        }
        printf("\n");
    }

    // Libera a memória alocada para a matriz
    for (int i = 0; i < linhas; i++) {
        free(matriz[i]);
    }
    free(matriz);

    return 0;
}
-------------------------------------------------------------
/* 15.Faça um programa que leia dois números N e M e:
a) Crie e leia uma matriz de inteiros N x M;
b) Localize os três maiores números de uma matriz e mostre a linha e a
coluna onde estão*/
#include <stdio.h>
#include <stdlib.h>

void localizarMaioresNumeros(int **matriz, int linhas, int colunas) {
    int maioresNumeros[3] = {0}; // Array para armazenar os três maiores números
    int linhaMaiores[3] = {0}; // Array para armazenar as linhas dos maiores números
    int colunaMaiores[3] = {0}; // Array para armazenar as colunas dos maiores números

    // Percorre a matriz e atualiza os maiores números encontrados
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            int numero = matriz[i][j];

            // Compara o número atual com os maiores números encontrados
            for (int k = 0; k < 3; k++) {
                if (numero > maioresNumeros[k]) {
                    // Desloca os valores anteriores para dar lugar ao novo maior número
                    for (int l = 2; l > k; l--) {
                        maioresNumeros[l] = maioresNumeros[l - 1];
                        linhaMaiores[l] = linhaMaiores[l - 1];
                        colunaMaiores[l] = colunaMaiores[l - 1];
                    }

                    // Armazena o novo maior número
                    maioresNumeros[k] = numero;
                    linhaMaiores[k] = i;
                    colunaMaiores[k] = j;

                    break;
                }
            }
        }
    }

    // Imprime as informações dos maiores números
    printf("Os três maiores números da matriz são:\n");
    for (int i = 0; i < 3; i++) {
        printf("Número: %d, Linha: %d, Coluna: %d\n", maioresNumeros[i], linhaMaiores[i], colunaMaiores[i]);
    }
}

int main() {
    int N, M;

    printf("Digite o número de linhas da matriz: ");
    scanf("%d", &N);

    printf("Digite o número de colunas da matriz: ");
    scanf("%d", &M);

    // Aloca espaço para a matriz
    int **matriz = (int **)malloc(N * sizeof(int *));
    if (matriz == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    for (int i = 0; i < N; i++) {
        matriz[i] = (int *)malloc(M * sizeof(int));
        if (matriz[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Preenche a matriz com os valores informados pelo usuário
    printf("Digite os valores da matriz:\n");
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            scanf("%d", &matriz[i][j]);
        }
    }

    // Chama a função localizarMaioresNumeros para encontrar os três maiores números da matriz
    localizarMaioresNumeros(matriz, N, M);

    // Libera a memória alocada para a matriz
    for (int i = 0; i < N; i++) {
        free(matriz[i]);
    }
    free(matriz);

    return 0;
}
----------------------------------------------------------------------------------------------------
/* 16.Faça um programa que leia dois números N e M:
a) Crie e leia uma matriz N x M de inteiros;
b) Crie e construa uma matriz transposta M x N de inteiros;
c) Mostre as duas matrizes.*/
#include <stdio.h>
#include <stdlib.h>

void imprimirMatriz(int **matriz, int linhas, int colunas) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            printf("%d ", matriz[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int N, M;

    printf("Digite o número de linhas da matriz: ");
    scanf("%d", &N);

    printf("Digite o número de colunas da matriz: ");
    scanf("%d", &M);

    // Criação da matriz N x M
    int **matriz = (int **)malloc(N * sizeof(int *));
    if (matriz == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    for (int i = 0; i < N; i++) {
        matriz[i] = (int *)malloc(M * sizeof(int));
        if (matriz[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Leitura dos valores da matriz
    printf("Digite os valores da matriz:\n");
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            scanf("%d", &matriz[i][j]);
        }
    }

    // Criação da matriz transposta M x N
    int **transposta = (int **)malloc(M * sizeof(int *));
    if (transposta == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    for (int i = 0; i < M; i++) {
        transposta[i] = (int *)malloc(N * sizeof(int));
        if (transposta[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Construção da matriz transposta
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            transposta[i][j] = matriz[j][i];
        }
    }

    // Impressão das matrizes
    printf("Matriz original:\n");
    imprimirMatriz(matriz, N, M);

    printf("Matriz transposta:\n");
    imprimirMatriz(transposta, M, N);

    // Liberação de memória
    for (int i = 0; i < N; i++) {
        free(matriz[i]);
    }
    free(matriz);

    for (int i = 0; i < M; i++) {
        free(transposta[i]);
    }
    free(transposta);

    return 0;
}
‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑‑
/* 17.Faça um programa que leia números do teclado e os armazene em um
vetor alocado dinamicamente. O usuário irá digitar uma sequência de
números, sem limite de quantidade. Os números serão digitados um a
um e, sendo que caso ele deseje encerrar a entrada de dados, ele irá
digitar o número ZERO. Os dados devem ser armazenados na memória
deste modo:
a) Inicie com um vetor de tamanho 10 alocado dinamicamente;
b) Após, caso o vetor alocado esteja cheio, aloque um novo vetor do
tamanho do vetor anterior adicionado espaço para mais 10 valores
(tamanho N+10, onde N inicia com 10);
c) Copie os valores já digitados da área inicial para esta área maior e
libere a memória da área inicial;
d) Repita este procedimento de expandir dinamicamente com mais 10
valores o vetor alocado cada vez que o mesmo estiver cheio. Assim o
vetor irá ser “expandido” de 10 em 10 valores.
Ao fnal, exiba o vetor lido. Não use a função REALLOC.*/
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *vetor = malloc(10 * sizeof(int));  // Vetor inicial com tamanho 10
    int tamanho = 10;  // Tamanho atual do vetor
    int indice = 0;  // Índice para percorrer o vetor
    int numero;

    printf("Digite os numeros (0 para sair):\n");

    while (1) {
        scanf("%d", &numero);

        if (numero == 0) {
            break;  // Sai do loop quando o número digitado for zero
        }

        vetor[indice++] = numero;

        if (indice == tamanho) {
            // O vetor está cheio, aloca um novo vetor com mais espaço
            int *novo_vetor = malloc((tamanho + 10) * sizeof(int));

            // Copia os valores do vetor original para o novo vetor
            for (int i = 0; i < tamanho; i++) {
                novo_vetor[i] = vetor[i];
            }

            // Libera a memória ocupada pelo vetor original
            free(vetor);

            vetor = novo_vetor;
            tamanho += 10;  // Atualiza o novo tamanho do vetor
        }
    }

    printf("Vetor lido:\n");
    for (int i = 0; i < indice; i++) {
        printf("%d ", vetor[i]);
    }
    printf("\n");

    // Libera a memória ocupada pelo vetor final
    free(vetor);

    return 0;
}
-------------------------------------------------------------------------------
/* 18.Escreva um programa para fazer a alocação dinâmica dos blocos de
dados conforme solicitado abaixo:
a) Vetor de 1024 Bytes (1 Kbyte);
b) Matriz de inteiros de dimensão 10 × 10;
c) Vetor para armazenar 50 registros contendo: nome do produto (30
caracteres), código do produto (inteiro) e preço em reais;
d) Texto de até 100 linhas com até 80 caracteres em cada linha.*/
#include <stdio.h>
#include <stdlib.h>

int main() {
    // a) Vetor de 1024 Bytes (1 Kbyte)
    int tamanhoVetor = 1024;
    char* vetor = (char*) malloc(tamanhoVetor * sizeof(char));
    if (vetor == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }

    // b) Matriz de inteiros de dimensão 10x10
    int linhas = 10;
    int colunas = 10;
    int** matriz = (int**) malloc(linhas * sizeof(int*));
    if (matriz == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }
    for (int i = 0; i < linhas; i++) {
        matriz[i] = (int*) malloc(colunas * sizeof(int));
        if (matriz[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // c) Vetor para armazenar 50 registros
    int tamanhoRegistro = 30 + sizeof(int) + sizeof(float);
    int quantidadeRegistros = 50;
    char** registros = (char**) malloc(quantidadeRegistros * sizeof(char*));
    if (registros == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }
    for (int i = 0; i < quantidadeRegistros; i++) {
        registros[i] = (char*) malloc(tamanhoRegistro * sizeof(char));
        if (registros[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // d) Texto de até 100 linhas com até 80 caracteres em cada linha
    int quantidadeLinhas = 100;
    int tamanhoLinha = 80;
    char** texto = (char**) malloc(quantidadeLinhas * sizeof(char*));
    if (texto == NULL) {
        printf("Erro de alocação de memória.\n");
        return 1;
    }
    for (int i = 0; i < quantidadeLinhas; i++) {
        texto[i] = (char*) malloc(tamanhoLinha * sizeof(char));
        if (texto[i] == NULL) {
            printf("Erro de alocação de memória.\n");
            return 1;
        }
    }

    // Liberação de memória
    free(vetor);

    for (int i = 0; i < linhas; i++) {
        free(matriz[i]);
    }
    free(matriz);

    for (int i = 0; i < quantidadeRegistros; i++) {
        free(registros[i]);
    }
    free(registros);

    for (int i = 0; i < quantidadeLinhas; i++) {
        free(texto[i]);
    }
    free(texto);

    return 0;
}
-------------------------------------------------------------------
/* 19.Faça um programa para associar nomes as linhas de uma matriz de
caracteres. O usuário irá informar o número máximo de nomes que
poderão ser armazenados. Cada nome poderá ter até 30 caracteres com
o '\0'. O usuário poderá usar 5 opções diferentes para manipular a
matriz:
a) Gravar um nome em uma linha da matriz;
b) Apagar o nome contido em uma linha da matriz;
c) Informar um nome, procurar a linha onde ele se encontra e substituir
por outro nome;
d) Informar um nome, procurar a linha onde ele se encontra e apagar;
e) Pedir para recuperar o nome contido em uma linha da matriz.*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOMES 5
#define TAMANHO_NOME 31

void imprimirMatriz(char matriz[MAX_NOMES][TAMANHO_NOME]) {
    for (int i = 0; i < MAX_NOMES; i++) {
        printf("Linha %d: %s\n", i+1, matriz[i]);
    }
}

int main() {
    char matriz[MAX_NOMES][TAMANHO_NOME];
    char nome[TAMANHO_NOME];
    int opcao, linha;

    // Inicializar matriz com nomes vazios
    for (int i = 0; i < MAX_NOMES; i++) {
        matriz[i][0] = '\0';
    }

    while (1) {
        printf("\n1 - Gravar nome em uma linha\n");
        printf("2 - Apagar nome de uma linha\n");
        printf("3 - Substituir nome em uma linha\n");
        printf("4 - Apagar linha por nome\n");
        printf("5 - Recuperar nome de uma linha\n");
        printf("0 - Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 0:
                printf("Saindo do programa.\n");
                return 0;

            case 1:
                printf("Digite o nome a ser gravado: ");
                scanf(" %[^\n]", nome);

                printf("Digite o número da linha (1 a %d): ", MAX_NOMES);
                scanf("%d", &linha);
                linha--;

                if (linha >= 0 && linha < MAX_NOMES) {
                    strncpy(matriz[linha], nome, TAMANHO_NOME);
                    matriz[linha][TAMANHO_NOME - 1] = '\0';
                    printf("Nome gravado com sucesso!\n");
                } else {
                    printf("Linha inválida.\n");
                }
                break;

            case 2:
                printf("Digite o número da linha (1 a %d) para apagar o nome: ", MAX_NOMES);
                scanf("%d", &linha);
                linha--;

                if (linha >= 0 && linha < MAX_NOMES) {
                    matriz[linha][0] = '\0';
                    printf("Nome apagado com sucesso!\n");
                } else {
                    printf("Linha inválida.\n");
                }
                break;

            case 3:
                printf("Digite o nome a ser substituído: ");
                scanf(" %[^\n]", nome);

                printf("Digite o número da linha (1 a %d) onde o nome está: ", MAX_NOMES);
                scanf("%d", &linha);
                linha--;

                if (linha >= 0 && linha < MAX_NOMES) {
                    strncpy(matriz[linha], nome, TAMANHO_NOME);
                    matriz[linha][TAMANHO_NOME - 1] = '\0';
                    printf("Nome substituído com sucesso!\n");
                } else {
                    printf("Linha inválida.\n");
                }
                break;

            case 4:
                printf("Digite o nome a ser buscado para apagar a linha: ");
                scanf(" %[^\n]", nome);

                for (int i = 0; i < MAX_NOMES; i++) {
                    if (strcmp(matriz[i], nome) == 0) {
                        matriz[i][0] = '\0';
                        printf("Nome encontrado na linha %d e linha apagada.\n", i+1);
                        break;
                    }
                }
                break;

            case 5:
                printf("Digite o número da linha (1 a %d) para recuperar o nome: ", MAX_NOMES);
                scanf("%d", &linha);
                linha--;

                if (linha >= 0 && linha < MAX_NOMES) {
                    printf("Nome na linha %d: %s\n", linha+1, matriz[linha]);
                } else {
                    printf("Linha inválida.\n");
                }
                break;

            default:
                printf("Opção inválida. Tente novamente.\n");
        }

        imprimirMatriz(matriz);
    }

    return 0;
}
-----------------------------------------------------------------------------------
/* 20.Faça um programa que:
a) Peça para o usuário entrar com o nome e a posição (coordenadas X e
Y) de N cidades e as armazene em um vetor de estruturas (N é
informado pelo usuário);
b) Crie uma matriz de distâncias entre cidades de tamanho N x N;
c) Calcule as distâncias entre cada duas cidades e armazene na matriz;
d) Exiba na tela a matriz de distancias obtida;
e) Quando o usuário digitar o número de duas cidades o programa
deverá retornar a distância entre elas.*/
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

typedef struct {
    char nome[30];
    int x;
    int y;
} Cidade;

double calcularDistancia(Cidade cidade1, Cidade cidade2) {
    int deltaX = cidade1.x - cidade2.x;
    int deltaY = cidade1.y - cidade2.y;
    return sqrt(deltaX * deltaX + deltaY * deltaY);
}

int main() {
    int N;

    printf("Digite a quantidade de cidades: ");
    scanf("%d", &N);

    // Alocar vetor de cidades
    Cidade *cidades = (Cidade*) malloc(N * sizeof(Cidade));

    // Ler informações das cidades
    for (int i = 0; i < N; i++) {
        printf("\nCidade %d:\n", i+1);
        printf("Nome: ");
        scanf(" %[^\n]", cidades[i].nome);
        printf("Posição X: ");
        scanf("%d", &cidades[i].x);
        printf("Posição Y: ");
        scanf("%d", &cidades[i].y);
    }

    // Alocar matriz de distâncias
    double **distancias = (double**) malloc(N * sizeof(double*));
    for (int i = 0; i < N; i++) {
        distancias[i] = (double*) malloc(N * sizeof(double));
    }

    // Calcular distâncias entre cidades e armazenar na matriz
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (i == j) {
                distancias[i][j] = 0.0;
            } else {
                distancias[i][j] = calcularDistancia(cidades[i], cidades[j]);
            }
        }
    }

    // Exibir a matriz de distâncias
    printf("\nMatriz de distâncias:\n");
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%.2lf\t", distancias[i][j]);
        }
        printf("\n");
    }

    // Calcular distância entre duas cidades
    int cidade1, cidade2;
    printf("\nDigite o número das duas cidades (1 a %d) para obter a distância entre elas: ", N);
    scanf("%d %d", &cidade1, &cidade2);
    cidade1--;
    cidade2--;

    if (cidade1 >= 0 && cidade1 < N && cidade2 >= 0 && cidade2 < N) {
        double distancia = distancias[cidade1][cidade2];
        printf("A distância entre %s e %s é %.2lf\n", cidades[cidade1].nome, cidades[cidade2].nome, distancia);
    } else {
        printf("Cidades inválidas.\n");
    }

    // Liberar memória alocada
    for (int i = 0; i < N; i++) {
        free(distancias[i]);
    }
    free(distancias);
    free(cidades);

    return 0;
}
-------------------------------------------------------------------------------------------
/* 21.Faça um programa que leia quatro números a, b, c e d, que serão as
dimensões de duas matrizes, e:
a) Crie e leia uma matriz, dadas as dimensões dela;
b) Crie e construa uma matriz que seja o produto de duas matrizes. Na
sua função main(), imprima as duas matrizes e o produto entre elas,
se existir.*/
#include <stdio.h>
#include <stdlib.h>

void lerMatriz(int **matriz, int linhas, int colunas) {
    printf("Digite os elementos da matriz:\n");
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            printf("Elemento [%d][%d]: ", i+1, j+1);
            scanf("%d", &matriz[i][j]);
        }
    }
}

void multiplicarMatrizes(int **matriz1, int **matriz2, int **produto, int linhas1, int colunas1, int colunas2) {
    for (int i = 0; i < linhas1; i++) {
        for (int j = 0; j < colunas2; j++) {
            produto[i][j] = 0;
            for (int k = 0; k < colunas1; k++) {
                produto[i][j] += matriz1[i][k] * matriz2[k][j];
            }
        }
    }
}

void imprimirMatriz(int **matriz, int linhas, int colunas) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            printf("%d\t", matriz[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int a, b, c, d;

    printf("Digite as dimensões da matriz A (linhas e colunas): ");
    scanf("%d %d", &a, &b);
    printf("Digite as dimensões da matriz B (linhas e colunas): ");
    scanf("%d %d", &c, &d);

    if (b != c) {
        printf("As dimensões das matrizes não são compatíveis para a multiplicação.\n");
        return 0;
    }

    int **matrizA = (int**) malloc(a * sizeof(int*));
    int **matrizB = (int**) malloc(c * sizeof(int*));
    int **produto = (int**) malloc(a * sizeof(int*));

    for (int i = 0; i < a; i++) {
        matrizA[i] = (int*) malloc(b * sizeof(int));
        produto[i] = (int*) malloc(d * sizeof(int));
    }

    for (int i = 0; i < c; i++) {
        matrizB[i] = (int*) malloc(d * sizeof(int));
    }

    printf("\nMatriz A:\n");
    lerMatriz(matrizA, a, b);

    printf("\nMatriz B:\n");
    lerMatriz(matrizB, c, d);

    multiplicarMatrizes(matrizA, matrizB, produto, a, b, d);

    printf("\nMatriz A:\n");
    imprimirMatriz(matrizA, a, b);

    printf("\nMatriz B:\n");
    imprimirMatriz(matrizB, c, d);

    printf("\nProduto das matrizes A e B:\n");
    imprimirMatriz(produto, a, d);

    for (int i = 0; i < a; i++) {
        free(matrizA[i]);
        free(produto[i]);
    }

    for (int i = 0; i < c; i++) {
        free(matrizB[i]);
    }

    free(matrizA);
    free(matrizB);
    free(produto);

    return 0;
}
