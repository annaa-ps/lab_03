1. Escreva um programa que:
a) Crie/abra um arquivo texto de nome “arq.txt”;
b) Permita que o usuário grave diversos caracteres nesse arquivo, até
que o usuário entre com o caractere ‘0’;
c) Feche o arquivo.

#include <stdio.h>
#include <stdlib.h>

int main() {
	FILE *arq;
	arq = fopen("./arquivos/arquivo-02.txt", "w");
	
	if (arq == NULL) {
		perror("\nHouve um erro ao criar o arquivo: ");
		exit(1);
	}
	
	char c;
	while(1) {
		printf("\nInforme um caractere para ser gravado (0 para sair): ");
		fflush(stdin);
		scanf("%c", &c);
		if (c == '0') break;
		fputc(c, arq);
	};
	
	fclose(arq);
	
	printf("\nArquivo fechado para gravacao!");
	
	arq = fopen("./arquivos/arquivo-02.txt", "r");
	
	if (arq == NULL) {
		perror("\nHouve um erro ao abrir arquivo para leitura: ");
		exit(1);
	}
	
	printf("\nArquivo aberto para leitura!");
	
	printf("\n\nConteudo: ");
	while ((c = fgetc(arq))!= EOF)
		printf("%c", c);
	
	printf("\n\n");
	
	fclose(arq);
	
	return 0;
}
-----------------------------------------------------------------
2. Faça um programa que receba do usuário um arquivo texto e mostre na
tela quantas linhas esse arquivo possui.
#include <stdio.h>
#include <stdlib.h>

int main(){
    FILE *arq;
    int linha = 0;
    /*abertura do arquivo*/
    arq = fopen("arq.txt", "r");
    if(arq == NULL){
        printf("Erro ao abrir o arquivo.");
        return 1;
    }
    /*sera executado a leitura de caracteres até qo fim do arquivo*/
    while(!feof(arq)){
        /*leitura feita caractere por caractere*/
        if(getc(arq) == '\n')
            linha ++;
    }
    printf("Arquivo tem %d linhas", linha);
    /*fechamento do arquivo*/
    fclose(arq);
    return 0;
}
-------------------------------------------------------------
3. Faça um programa que receba do usuário um arquivo texto e mostre na
tela quantas letras são vogais.
#include <stdio.h>
#include <stdlib.h>


int main(){
    FILE *arq;
    int vogal = 0, consoante = 0;
    int c;
    /*abertura do arquivo*/
    arq = fopen("arq.txt", "r+");
    if(arq == NULL){
        printf("Erro ao abrir o arquivo.");
        return 1;
    }
    /*sera executado a leitura de caracteres até qo fim do arquivo*/
    while(feof(arq) == 0){
        /*leitura feita caractere por caractere*/
        c = getc(arq);
		/*contagem das vogais*/
        if(c == 'a' || c == 'A' || c == 'e' || c == 'E' || c == 'i' || c == 'I' || c == 'o' || c == 'O'|| c == 'u'|| c == 'U'){
            vogal ++;
			/*contagem das consoantes*/
        }else if(c != ' '&& c!='ÿ' && c != '\n' && c != '0' && c != '1' && c != '2' && c != '3' && 
		c != '4' && c != '5' && c != '6' && c != '7' && c != '8' && c != '9')
                consoante ++;
        printf("%c",c);

    }
   printf("\nArquivo tem %d vogais e %d consoantes", vogal, consoante);
    /*fechamento do arquivo*/
    fclose(arq);
    return 0;
}
----------------------------------------------------------------
4. Faça um programa que receba do usuário um arquivo texto e mostre na
tela quantas letras são vogais e quantas são consoantes
#include <stdio.h>
#include <ctype.h>

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    char caractere;
    int vogais = 0, consoantes = 0;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while ((caractere = fgetc(arquivo)) != EOF) {
        caractere = tolower(caractere);  // Convertendo para minúsculas

        if (isalpha(caractere)) {  // Verificando se é uma letra
            if (caractere == 'a' || caractere == 'e' || caractere == 'i' || caractere == 'o' || caractere == 'u') {
                vogais++;
            } else {
                consoantes++;
            }
        }
    }

    fclose(arquivo);

    printf("Quantidade de vogais: %d\n", vogais);
    printf("Quantidade de consoantes: %d\n", consoantes);

    return 0;
}
----------------------------------------------------------------
5. Faça um programa que receba do usuário um arquivo texto e um
caractere. Mostre na tela quantas vezes aquele caractere ocorre dentro
do arquivo.
#include <stdio.h>

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    char caractere;
    int ocorrencias = 0;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    printf("Digite o caractere a ser buscado: ");
    scanf(" %c", &caractere);  // Nota: o espaço antes de %c é importante para ignorar possíveis caracteres de espaço em branco

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while (!feof(arquivo)) {
        char c = fgetc(arquivo);

        if (c == caractere) {
            ocorrencias++;
        }
    }

    fclose(arquivo);

    printf("O caractere '%c' ocorre %d vezes no arquivo.\n", caractere, ocorrencias);

    return 0;
}
----------------------------------------------------------------
6. Faça um programa que receba do usuário um arquivo texto e mostre na
tela quantas vezes cada letra do alfabeto aparece dentro do arquivo.
#include <stdio.h>
#include <ctype.h>

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    int contagem[26] = {0};
    char caractere;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while ((caractere = fgetc(arquivo)) != EOF) {
        caractere = tolower(caractere);  // Convertendo para minúsculas

        if (isalpha(caractere)) {  // Verificando se é uma letra
            contagem[caractere - 'a']++;  // Incrementando o contador correspondente
        }
    }

    fclose(arquivo);

    printf("Contagem de letras:\n");
    for (int i = 0; i < 26; i++) {
        printf("%c: %d\n", 'a' + i, contagem[i]);
    }

    return 0;
}
----------------------------------------------------------------
7. Faça um programa que receba do usuário um arquivo texto. Crie outro
arquivo texto contendo o texto do arquivo de entrada, mas com as
vogais substituídas por ‘*’
#include <stdio.h>
#include <stdlib.h>


int main(){
    FILE *arq1, *arq2;
    char c;
    /*abertura do arquivo para leitura*/
    arq1 = fopen("arq.txt", "r");
    if(arq1 == NULL){
        printf("Erro ao abrir o arquivo de leitura.");
        return 1;
    }
	 /*abertura do arquivo para escrita*/
    arq2 = fopen("arq2.txt", "w");
    if(arq1 == NULL){
        printf("Erro ao abrir o arquivo de escrita.");
        return 1;
    }
    /*sera executado a leitura dos caracteres de arq.txt até seu fim*/
    while(feof(arq1) == 0){
        /*leitura feita caractere por caractere*/
        c = getc(arq1);
		/*substituição das vogais por '*' */
        if(c == 'a' || c == 'A' || c == 'e' || c == 'E' || c == 'i' || c == 'I' || c == 'o' || c == 'O'|| c == 'u'|| c == 'U'){
            c = '*';
            fprintf(arq2,"%c", c);
			/*impressão dos outros caracteres*/
        }else if(c != 'ÿ')
            fprintf(arq2,"%c", c);


    }
	/*fechamento dos arquivos utilizadps*/
    fclose(arq1);
    fclose(arq2);
    return 0;
}
-----------------------------------------------------------
8. Faça um programa que leia o conteúdo de um arquivo e crie um arquivo
com o mesmo conteúdo, mas com todas as letras minúsculas
convertidas para maiúsculas. Os nomes dos arquivos serão fornecidos,
via teclado, pelo usuário. A função que converte maiúscula para
minúscula é o toupper(). Ela é aplicada em cada caractere da string
#include <stdio.h>
#include <ctype.h>

int main() {
    FILE *arquivoEntrada, *arquivoSaida;
    char nomeArquivoEntrada[100], nomeArquivoSaida[100];
    char caractere;

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    arquivoEntrada = fopen(nomeArquivoEntrada, "r");

    if (arquivoEntrada == NULL) {
        printf("Erro ao abrir o arquivo de entrada.\n");
        return 1;
    }

    arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoSaida == NULL) {
        printf("Erro ao abrir o arquivo de saída.\n");
        fclose(arquivoEntrada);
        return 1;
    }

    while ((caractere = fgetc(arquivoEntrada)) != EOF) {
        caractere = toupper(caractere);  // Convertendo para maiúsculas
        fputc(caractere, arquivoSaida);
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo convertido com sucesso.\n");

    return 0;
}
------------------------------------------------------
9. Faça um programa que receba dois arquivos do usuário, e crie um
terceiro arquivo com o conteúdo dos dois primeiros juntos (o conteúdo
do primeiro seguido do conteúdo do segundo).
#include <stdio.h>

int main() {
    FILE *arquivo1, *arquivo2, *arquivo3;
    char nomeArquivo1[100], nomeArquivo2[100], nomeArquivo3[100];
    char caractere;

    printf("Digite o nome do primeiro arquivo: ");
    scanf("%s", nomeArquivo1);

    printf("Digite o nome do segundo arquivo: ");
    scanf("%s", nomeArquivo2);

    printf("Digite o nome do terceiro arquivo: ");
    scanf("%s", nomeArquivo3);

    arquivo1 = fopen(nomeArquivo1, "r");

    if (arquivo1 == NULL) {
        printf("Erro ao abrir o primeiro arquivo.\n");
        return 1;
    }

    arquivo2 = fopen(nomeArquivo2, "r");

    if (arquivo2 == NULL) {
        printf("Erro ao abrir o segundo arquivo.\n");
        fclose(arquivo1);
        return 1;
    }

    arquivo3 = fopen(nomeArquivo3, "w");

    if (arquivo3 == NULL) {
        printf("Erro ao criar o terceiro arquivo.\n");
        fclose(arquivo1);
        fclose(arquivo2);
        return 1;
    }

    while ((caractere = fgetc(arquivo1)) != EOF) {
        fputc(caractere, arquivo3);
    }

    while ((caractere = fgetc(arquivo2)) != EOF) {
        fputc(caractere, arquivo3);
    }

    fclose(arquivo1);
    fclose(arquivo2);
    fclose(arquivo3);

    printf("Arquivo criado com sucesso.\n");

    return 0;
}
--------------------------------------------------------------
10.Faça um programa que receba o nome de um arquivo de entrada e outro
de saída. O arquivo de entrada contém em cada linha o nome de uma
cidade (ocupando 40 caracteres) e o seu número de habitantes. O
programa deverá ler o arquivo de entrada e gerar um arquivo de 
saídaonde aparece o nome da cidade mais populosa seguida pelo seu número
de habitantes.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME_CIDADE 41

int main() {
    FILE *arquivoEntrada, *arquivoSaida;
    char nomeArquivoEntrada[100], nomeArquivoSaida[100];
    char nomeCidade[MAX_NOME_CIDADE];
    int populacao, maiorPopulacao = 0;
    char cidadeMaisPopulosa[MAX_NOME_CIDADE];

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    arquivoEntrada = fopen(nomeArquivoEntrada, "r");

    if (arquivoEntrada == NULL) {
        printf("Erro ao abrir o arquivo de entrada.\n");
        return 1;
    }

    arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoSaida == NULL) {
        printf("Erro ao abrir o arquivo de saída.\n");
        fclose(arquivoEntrada);
        return 1;
    }

    while (fscanf(arquivoEntrada, "%40s %d", nomeCidade, &populacao) == 2) {
        if (populacao > maiorPopulacao) {
            maiorPopulacao = populacao;
            strcpy(cidadeMaisPopulosa, nomeCidade);
        }
    }

    fprintf(arquivoSaida, "Cidade mais populosa: %s\n", cidadeMaisPopulosa);
    fprintf(arquivoSaida, "Populacao: %d\n", maiorPopulacao);

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo gerado com sucesso.\n");

    return 0;
}
--------------------------------------------------------------
11.Faça um programa no qual o usuário informa o nome do arquivo e uma
palavra, e retorne o número de vezes que aquela palavra aparece no
arquivo.
#include <stdio.h>
#include <string.h>

#define MAX_TAMANHO_PALAVRA 100

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    char palavra[MAX_TAMANHO_PALAVRA];
    char palavraArquivo[MAX_TAMANHO_PALAVRA];
    int contador = 0;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    printf("Digite a palavra a ser pesquisada: ");
    scanf("%s", palavra);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while (fscanf(arquivo, "%s", palavraArquivo) != EOF) {
        if (strcmp(palavraArquivo, palavra) == 0) {
            contador++;
        }
    }

    fclose(arquivo);

    printf("A palavra '%s' aparece %d vezes no arquivo.\n", palavra, contador);

    return 0;
}
-------------------------------------------------------
12.Abra um arquivo texto, calcule e escreva o número de caracteres, o
número de linhas e o número de palavras neste arquivo. Escreva
também quantas vezes cada letra ocorre no arquivo (ignorando letras
com acento). Obs.: palavras são separadas por um ou mais caracteres
espaço, tabulação ou nova linha.
#include <stdio.h>
#include <ctype.h>

#define MAX_TAMANHO_ARQUIVO 1000000

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    char texto[MAX_TAMANHO_ARQUIVO];
    int numCaracteres = 0;
    int numLinhas = 0;
    int numPalavras = 0;
    int frequencia[26] = {0};  // Frequência de cada letra (de A a Z)

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    // Calcula o número de caracteres, linhas e palavras
    while (fgets(texto, MAX_TAMANHO_ARQUIVO, arquivo) != NULL) {
        numCaracteres += strlen(texto);
        numLinhas++;

        int i = 0;
        while (texto[i] != '\0') {
            if (!isspace(texto[i])) {
                numPalavras++;
                while (texto[i] != '\0' && !isspace(texto[i])) {
                    i++;
                }
            } else {
                i++;
            }
        }
    }

    // Calcula a frequência de cada letra (ignorando letras com acento)
    fseek(arquivo, 0, SEEK_SET);  // Reinicia o ponteiro do arquivo para o início
    while (fgets(texto, MAX_TAMANHO_ARQUIVO, arquivo) != NULL) {
        int i = 0;
        while (texto[i] != '\0') {
            if (isalpha(texto[i])) {
                char letra = toupper(texto[i]);
                frequencia[letra - 'A']++;
            }
            i++;
        }
    }

    fclose(arquivo);

    printf("Número de caracteres: %d\n", numCaracteres);
    printf("Número de linhas: %d\n", numLinhas);
    printf("Número de palavras: %d\n", numPalavras);

    printf("Frequência de cada letra:\n");
    for (int i = 0; i < 26; i++) {
        printf("%c: %d\n", 'A' + i, frequencia[i]);
    }

    return 0;
}
-----------------------------------------------------------
13.Faça um programa que permita que o usuário entre com diversos nomes
e telefone para cadastro, e crie um arquivo com essas informações, uma
por linha. O usuário fnaliza a entrada com ‘0’ para o telefone.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 100
#define MAX_TELEFONE 20

int main() {
    FILE *arquivo;
    char nome[MAX_NOME];
    char telefone[MAX_TELEFONE];

    arquivo = fopen("cadastro.txt", "w");

    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return 1;
    }

    while (1) {
        printf("Digite o nome (ou '0' para sair): ");
        fgets(nome, MAX_NOME, stdin);
        nome[strcspn(nome, "\n")] = '\0';  // Remove a quebra de linha

        if (strcmp(nome, "0") == 0) {
            break;
        }

        printf("Digite o telefone: ");
        fgets(telefone, MAX_TELEFONE, stdin);
        telefone[strcspn(telefone, "\n")] = '\0';  // Remove a quebra de linha

        if (strcmp(telefone, "0") == 0) {
            break;
        }

        fprintf(arquivo, "%s %s\n", nome, telefone);
    }

    fclose(arquivo);

    printf("Arquivo de cadastro criado com sucesso.\n");

    return 0;
}
----------------------------------------------------
14.Dado um arquivo contendo um conjunto de nome e data de nascimento
(DD MM AAAA), isto é, 3 inteiros em sequência), faça um programa que
leia o nome do arquivo e a data de hoje e construa outro arquivo
contendo o nome e a idade de cada pessoa do primeiro arquivo.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_NOME 100

struct Pessoa {
    char nome[MAX_NOME];
    int dia;
    int mes;
    int ano;
};

int calcularIdade(int diaNascimento, int mesNascimento, int anoNascimento, int diaAtual, int mesAtual, int anoAtual) {
    int idade = anoAtual - anoNascimento;

    if (mesAtual < mesNascimento || (mesAtual == mesNascimento && diaAtual < diaNascimento)) {
        idade--;
    }

    return idade;
}

int main() {
    FILE *arquivoEntrada, *arquivoSaida;
    char nomeArquivoEntrada[100], nomeArquivoSaida[100];
    int diaAtual, mesAtual, anoAtual;
    struct Pessoa pessoa;

    // Obter a data atual
    time_t agora = time(NULL);
    struct tm *dataAtual = localtime(&agora);
    diaAtual = dataAtual->tm_mday;
    mesAtual = dataAtual->tm_mon + 1;
    anoAtual = dataAtual->tm_year + 1900;

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    arquivoEntrada = fopen(nomeArquivoEntrada, "r");

    if (arquivoEntrada == NULL) {
        printf("Erro ao abrir o arquivo de entrada.\n");
        return 1;
    }

    arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoSaida == NULL) {
        printf("Erro ao abrir o arquivo de saída.\n");
        fclose(arquivoEntrada);
        return 1;
    }

    while (fscanf(arquivoEntrada, "%s %d %d %d", pessoa.nome, &pessoa.dia, &pessoa.mes, &pessoa.ano) == 4) {
        int idade = calcularIdade(pessoa.dia, pessoa.mes, pessoa.ano, diaAtual, mesAtual, anoAtual);
        fprintf(arquivoSaida, "%s %d\n", pessoa.nome, idade);
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo de saída criado com sucesso.\n");

    return 0;
}
-------------------------------------------------------------------
15.Faça um programa que receba como entrada o ano corrente e o nome de
dois arquivos: um de entrada e outro de saída. Cada linha do arquivo de
entrada contém o nome de uma pessoa (ocupando 40 caracteres) e o
seu ano de nascimento. O programa deverá ler o arquivo de entrada e
gerar um arquivo de saída onde aparece o nome da pessoa seguida por
uma string que representa a sua idade.
- Se a idade for menor do que 18 anos, escreva “menor de idade”;
- Se a idade for maior do que 18 anos, escreva “maior de idade”;
- Se a idade for igual a 18 anos, escreva “entrando na maior idade”.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 40

int main() {
    FILE *arquivoEntrada, *arquivoSaida;
    char nomeArquivoEntrada[100], nomeArquivoSaida[100];
    int anoCorrente;

    printf("Digite o ano corrente: ");
    scanf("%d", &anoCorrente);

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    arquivoEntrada = fopen(nomeArquivoEntrada, "r");

    if (arquivoEntrada == NULL) {
        printf("Erro ao abrir o arquivo de entrada.\n");
        return 1;
    }

    arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoSaida == NULL) {
        printf("Erro ao abrir o arquivo de saída.\n");
        fclose(arquivoEntrada);
        return 1;
    }

    char nome[MAX_NOME];
    int anoNascimento;

    while (fscanf(arquivoEntrada, "%s %d", nome, &anoNascimento) == 2) {
        int idade = anoCorrente - anoNascimento;
        char statusIdade[20];

        if (idade < 18) {
            strcpy(statusIdade, "menor de idade");
        } else if (idade > 18) {
            strcpy(statusIdade, "maior de idade");
        } else {
            strcpy(statusIdade, "entrando na maior idade");
        }

        fprintf(arquivoSaida, "%s %s\n", nome, statusIdade);
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo de saída criado com sucesso.\n");

    return 0;
}
-----------------------------------------------------------
16.Faça um programa que recebe um vetor de 10 números, converta cada
um desses números para binário e grave a sequência de 0s e 1s em um
arquivo texto. Cada número deve ser gravado em uma linha.
#include <stdio.h>

void decimalParaBinario(int numero, char *binario) {
    int indice = 0;

    if (numero == 0) {
        binario[indice++] = '0';
    } else {
        while (numero > 0) {
            binario[indice++] = (numero % 2) + '0';
            numero /= 2;
        }
    }

    // Inverte o binário
    int i, j;
    for (i = 0, j = indice - 1; i < j; i++, j--) {
        char temp = binario[i];
        binario[i] = binario[j];
        binario[j] = temp;
    }

    binario[indice] = '\0';
}

int main() {
    int numeros[10];
    char binarios[10][33];  // Vetor de strings para armazenar os binários

    printf("Digite 10 números:\n");

    for (int i = 0; i < 10; i++) {
        printf("Número %d: ", i + 1);
        scanf("%d", &numeros[i]);
    }

    FILE *arquivo = fopen("binarios.txt", "w");

    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return 1;
    }

    for (int i = 0; i < 10; i++) {
        decimalParaBinario(numeros[i], binarios[i]);
        fprintf(arquivo, "%s\n", binarios[i]);
    }

    fclose(arquivo);

    printf("Arquivo 'binarios.txt' criado com sucesso.\n");

    return 0;
}
----------------------------------------------------
17.Faça um programa que leia um arquivo que contenha as dimensões de
uma matriz (linha e coluna), a quantidade de posições que serão
anuladas, e as posições a serem anuladas (linha e coluna). O programa
lê esse arquivo e, em seguida, produz um novo arquivo com a matriz
com as dimensões dadas no arquivo lido, e todas as posições
especifcadas no arquivo ZERADAS e o restante recebendo o valor 1.
Ex: arquivo “matriz.txt”
3 3 2 /*3 e 3 dimensoes da matriz e 2 posicoes que serao
anuladas*/
1 0
1 2 /*Posicoes da matriz que serao anuladas.
arquivo “matriz_saida.txt”
saída:
1 1 1
0 1 0
1 1 1
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
    FILE *arquivoEntrada, *arquivoSaida;
    char nomeArquivoEntrada[100], nomeArquivoSaida[100];
    int linhas, colunas, posicoesAnuladas;

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    arquivoEntrada = fopen(nomeArquivoEntrada, "r");

    if (arquivoEntrada == NULL) {
        printf("Erro ao abrir o arquivo de entrada.\n");
        return 1;
    }

    arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoSaida == NULL) {
        printf("Erro ao abrir o arquivo de saída.\n");
        fclose(arquivoEntrada);
        return 1;
    }

    fscanf(arquivoEntrada, "%d %d %d", &linhas, &colunas, &posicoesAnuladas);

    int **matriz = (int **)malloc(linhas * sizeof(int *));
    for (int i = 0; i < linhas; i++) {
        matriz[i] = (int *)malloc(colunas * sizeof(int));
    }

    // Inicializa a matriz com 1s
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            matriz[i][j] = 1;
        }
    }

    // Lê as posições a serem anuladas e zera na matriz
    for (int i = 0; i < posicoesAnuladas; i++) {
        int linha, coluna;
        fscanf(arquivoEntrada, "%d %d", &linha, &coluna);
        matriz[linha][coluna] = 0;
    }

    // Escreve a matriz no arquivo de saída
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            fprintf(arquivoSaida, "%d ", matriz[i][j]);
        }
        fprintf(arquivoSaida, "\n");
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo de saída criado com sucesso.\n");

    // Liberar memória alocada para a matriz
    for (int i = 0; i < linhas; i++) {
        free(matriz[i]);
    }
    free(matriz);

    return 0;
}
------------------------------------------------------------
18.Faça um programa que leia um arquivo contendo o nome e o preço de
diversos produtos (separados por linha), e calcule o total da compra.
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    char nomeProduto[100];
    float precoProduto;
    float totalCompra = 0;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while (fscanf(arquivo, "%s %f", nomeProduto, &precoProduto) == 2) {
        printf("Produto: %s\n", nomeProduto);
        printf("Preço: R$ %.2f\n", precoProduto);
        totalCompra += precoProduto;
    }

    fclose(arquivo);

    printf("Total da compra: R$ %.2f\n", totalCompra);

    return 0;
}
-----------------------------------------------------------
19.Faça um programa que receba do usuário um arquivo que contenha o
nome e a nota de diversos alunos (da seguinte forma: NOME: JOÃO
NOTA: 8), um aluno por linha. Mostre na tela o nome e a nota do aluno
que possui a maior nota.
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char nome[100];
    float nota;
} Aluno;

int main() {
    FILE *arquivo;
    char nomeArquivo[100];
    Aluno aluno;
    Aluno melhorAluno;
    float maiorNota = 0;

    printf("Digite o nome do arquivo: ");
    scanf("%s", nomeArquivo);

    arquivo = fopen(nomeArquivo, "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    while (fscanf(arquivo, "NOME: %s NOTA: %f", aluno.nome, &aluno.nota) == 2) {
        if (aluno.nota > maiorNota) {
            maiorNota = aluno.nota;
            melhorAluno = aluno;
        }
    }

    fclose(arquivo);

    printf("Aluno com a maior nota:\n");
    printf("Nome: %s\n", melhorAluno.nome);
    printf("Nota: %.2f\n", melhorAluno.nota);

    return 0;
}
--------------------------------------------------
20.Crie um programa que receba como entrada o número de alunos de uma
disciplina. Aloque dinamicamente dois vetores para armazenar as
informações a respeito desses alunos. O primeiro vetor contém o nome
dos alunos e o segundo contém suas notas fnais. Crie um arquivo que
armazene, a cada linha, o nome do aluno e sua nota fnal. Use nomes
com no máximo 40 caracteres. Se o nome não contém 40 caracteres,
complete com espaço em branco.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 40

int main() {
    int numAlunos;

    printf("Digite o número de alunos: ");
    scanf("%d", &numAlunos);

    // Alocação dinâmica dos vetores para armazenar os nomes e notas
    char **nomes = (char **)malloc(numAlunos * sizeof(char *));
    float *notas = (float *)malloc(numAlunos * sizeof(float));

    // Leitura dos nomes e notas dos alunos
    for (int i = 0; i < numAlunos; i++) {
        nomes[i] = (char *)malloc(MAX_NOME * sizeof(char));

        printf("Digite o nome do aluno %d: ", i + 1);
        scanf(" %[^\n]s", nomes[i]);

        printf("Digite a nota final do aluno %d: ", i + 1);
        scanf("%f", &notas[i]);
    }

    // Criação do arquivo e gravação dos dados
    FILE *arquivo = fopen("alunos.txt", "w");

    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return 1;
    }

    for (int i = 0; i < numAlunos; i++) {
        fprintf(arquivo, "%-*s %.2f\n", MAX_NOME, nomes[i], notas[i]);
    }

    fclose(arquivo);

    // Liberação da memória alocada
    for (int i = 0; i < numAlunos; i++) {
        free(nomes[i]);
    }
    free(nomes);
    free(notas);

    printf("Arquivo criado com sucesso.\n");

    return 0;
}
----------------------------------------------------------
21.Crie um programa que receba como entrada o número de alunos de uma
disciplina. Aloque dinamicamente em uma estrutura para armazenar as
informações a respeito desses alunos: nome do aluno e sua nota fnal.
Use nomes com no máximo 40 caracteres. Em seguida, salve os dados
dos alunos em um arquivo binário. Por fm, leia o arquivo e mostre o
nome do aluno com a maior nota.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 40

typedef struct {
    char nome[MAX_NOME];
    float nota;
} Aluno;

int main() {
    int numAlunos;

    printf("Digite o número de alunos: ");
    scanf("%d", &numAlunos);

    // Alocação dinâmica da estrutura para armazenar os dados dos alunos
    Aluno *alunos = (Aluno *)malloc(numAlunos * sizeof(Aluno));

    // Leitura dos dados dos alunos
    for (int i = 0; i < numAlunos; i++) {
        printf("Digite o nome do aluno %d: ", i + 1);
        scanf(" %[^\n]s", alunos[i].nome);

        printf("Digite a nota final do aluno %d: ", i + 1);
        scanf("%f", &alunos[i].nota);
    }

    // Salvando os dados dos alunos em um arquivo binário
    FILE *arquivo = fopen("alunos.bin", "wb");

    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return 1;
    }

    fwrite(alunos, sizeof(Aluno), numAlunos, arquivo);
    fclose(arquivo);

    // Leitura do arquivo e busca do aluno com a maior nota
    arquivo = fopen("alunos.bin", "rb");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    float maiorNota = 0;
    char nomeMaiorNota[MAX_NOME];

    for (int i = 0; i < numAlunos; i++) {
        fread(&alunos[i], sizeof(Aluno), 1, arquivo);
        if (alunos[i].nota > maiorNota) {
            maiorNota = alunos[i].nota;
            strcpy(nomeMaiorNota, alunos[i].nome);
        }
    }

    fclose(arquivo);

    printf("Aluno com a maior nota: %s\n", nomeMaiorNota);

    // Liberação da memória alocada
    free(alunos);

    return 0;
}
-----------------------------------------------------------
22.Faça um programa que recebe como entrada o nome de um arquivo de
entrada e o nome de um arquivo de saída. O arquivo de entrada contém
o nome de um aluno ocupando 40 caracteres e três inteiros que indicam
suas notas. O programa deverá ler o arquivo de entrada e gerar um
arquivo de saída onde aparece o nome do aluno e as suas notas em
ordem crescente.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 40

typedef struct {
    char nome[MAX_NOME];
    int notas[3];
} Aluno;

int compararNotas(const void *nota1, const void *nota2) {
    return (*(int *)nota1 - *(int *)nota2);
}

int main() {
    char nomeArquivoEntrada[100];
    char nomeArquivoSaida[100];

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    FILE *arquivoEntrada = fopen(nomeArquivoEntrada, "r");
    FILE *arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoEntrada == NULL || arquivoSaida == NULL) {
        printf("Erro ao abrir os arquivos.\n");
        return 1;
    }

    Aluno aluno;
    while (fscanf(arquivoEntrada, "%s %d %d %d", aluno.nome, &aluno.notas[0], &aluno.notas[1], &aluno.notas[2]) == 4) {
        // Ordena as notas em ordem crescente
        qsort(aluno.notas, 3, sizeof(int), compararNotas);

        // Escreve no arquivo de saída
        fprintf(arquivoSaida, "%-*s %d %d %d\n", MAX_NOME, aluno.nome, aluno.notas[0], aluno.notas[1], aluno.notas[2]);
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo de saída criado com sucesso.\n");

    return 0;
}
-------------------------------------------------------------------
23.Escreva um programa que leia a profssão e o tempo de serviço (em
anos) de cada um dos 5 funcionários de uma empresa e armazene-os no
arquivo “emp.txt”. Cada linha do arquivo corresponde aos dados de um
funcionário. Utilize o comando fprintf(). Em seguida, leia o mesmo
arquivo utilizando fscanf(). Apresente os dados na tela.
#include <stdio.h>

#define MAX_PROFISSAO 50

typedef struct {
    char profissao[MAX_PROFISSAO];
    int tempoServico;
} Funcionario;

int main() {
    Funcionario funcionarios[5];

    // Leitura dos dados dos funcionários
    for (int i = 0; i < 5; i++) {
        printf("Digite a profissão do funcionário %d: ", i + 1);
        scanf(" %[^\n]s", funcionarios[i].profissao);

        printf("Digite o tempo de serviço (em anos) do funcionário %d: ", i + 1);
        scanf("%d", &funcionarios[i].tempoServico);
    }

    // Gravação dos dados no arquivo
    FILE *arquivo = fopen("emp.txt", "w");

    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return 1;
    }

    for (int i = 0; i < 5; i++) {
        fprintf(arquivo, "%s %d\n", funcionarios[i].profissao, funcionarios[i].tempoServico);
    }

    fclose(arquivo);

    // Leitura dos dados do arquivo e apresentação na tela
    arquivo = fopen("emp.txt", "r");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return 1;
    }

    Funcionario funcionarioLido;
    printf("Dados dos funcionários:\n");
    while (fscanf(arquivo, "%s %d", funcionarioLido.profissao, &funcionarioLido.tempoServico) == 2) {
        printf("Profissão: %s\n", funcionarioLido.profissao);
        printf("Tempo de serviço: %d anos\n", funcionarioLido.tempoServico);
        printf("---------\n");
    }

    fclose(arquivo);

    return 0;
}
----------------------------------------------------------------
24.Implemente um controle simples de mercadorias em uma despensa
doméstica. Para cada produto armazene um código numérico, descrição
e quantidade atual. O programa deve ter opções para entrada e retirada
de produtos, bem como um relatório geral e um de produtos não
disponíveis. Armazene os dados em arquivo binário.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_DESCRICAO 50

typedef struct {
    int codigo;
    char descricao[MAX_DESCRICAO];
    int quantidade;
} Produto;

void exibirMenu() {
    printf("========== Despensa Doméstica ==========\n");
    printf("1. Entrada de Produto\n");
    printf("2. Retirada de Produto\n");
    printf("3. Relatório Geral\n");
    printf("4. Relatório de Produtos Não Disponíveis\n");
    printf("5. Sair\n");
    printf("========================================\n");
    printf("Escolha uma opção: ");
}

void entradaProduto(FILE *arquivo) {
    Produto produto;
    printf("Código do produto: ");
    scanf("%d", &produto.codigo);

    printf("Descrição do produto: ");
    scanf(" %[^\n]s", produto.descricao);

    printf("Quantidade do produto: ");
    scanf("%d", &produto.quantidade);

    fseek(arquivo, 0, SEEK_END);
    fwrite(&produto, sizeof(Produto), 1, arquivo);

    printf("Produto registrado com sucesso!\n");
}

void retiradaProduto(FILE *arquivo) {
    int codigo;
    printf("Código do produto a ser retirado: ");
    scanf("%d", &codigo);

    fseek(arquivo, 0, SEEK_SET);

    Produto produto;
    int encontrado = 0;
    while (fread(&produto, sizeof(Produto), 1, arquivo) == 1) {
        if (produto.codigo == codigo) {
            encontrado = 1;
            break;
        }
    }

    if (encontrado) {
        int quantidadeRetirada;
        printf("Quantidade a ser retirada: ");
        scanf("%d", &quantidadeRetirada);

        if (quantidadeRetirada <= produto.quantidade) {
            produto.quantidade -= quantidadeRetirada;
            fseek(arquivo, -sizeof(Produto), SEEK_CUR);
            fwrite(&produto, sizeof(Produto), 1, arquivo);
            printf("Produto retirado com sucesso!\n");
        } else {
            printf("Quantidade insuficiente no estoque.\n");
        }
    } else {
        printf("Produto não encontrado.\n");
    }
}

void relatorioGeral(FILE *arquivo) {
    printf("Relatório Geral:\n");

    fseek(arquivo, 0, SEEK_SET);

    Produto produto;
    while (fread(&produto, sizeof(Produto), 1, arquivo) == 1) {
        printf("Código: %d\n", produto.codigo);
        printf("Descrição: %s\n", produto.descricao);
        printf("Quantidade: %d\n", produto.quantidade);
        printf("-------------------------\n");
    }
}

void relatorioProdutosNaoDisponiveis(FILE *arquivo) {
    printf("Relatório de Produtos Não Disponíveis:\n");

    fseek(arquivo, 0, SEEK_SET);

    Produto produto;
    int naoDisponiveis = 0;
    while (fread(&produto, sizeof(Produto), 1, arquivo) == 1) {
        if (produto.quantidade == 0) {
            printf("Código: %d\n", produto.codigo);
            printf("Descrição: %s\n", produto.descricao);
            printf("-------------------------\n");
            naoDisponiveis++;
        }
    }

    if (naoDisponiveis == 0) {
        printf("Nenhum produto indisponível.\n");
    }
}

int main() {
    FILE *arquivo = fopen("despensa.bin", "rb+");

    if (arquivo == NULL) {
        arquivo = fopen("despensa.bin", "wb+");
        if (arquivo == NULL) {
            printf("Erro ao criar o arquivo.\n");
            return 1;
        }
    }

    int opcao;
    do {
        exibirMenu();
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                entradaProduto(arquivo);
                break;
            case 2:
                retiradaProduto(arquivo);
                break;
            case 3:
                relatorioGeral(arquivo);
                break;
            case 4:
                relatorioProdutosNaoDisponiveis(arquivo);
                break;
            case 5:
                printf("Encerrando o programa...\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
                break;
        }
    } while (opcao != 5);

    fclose(arquivo);

    return 0;
}
------------------------------------------------------------------------
25.Faça um programa gerenciar uma agenda de contatos. Para cada
contato armazene o nome, o telefone e o aniversário (dia e mês). O
programa deve permitir
 inserir contato;
 remover contato;
 pesquisar um contato pelo nome;
 listar todos os contatos;
 listar os contatos cujo nome inicia com uma dada letra;
 imprimir os aniversariantes do mês.
Sempre que o programa for encerrado, os contatos devem ser
armazenados em um arquivo binário. Quando o programa iniciar, os
contatos devem ser inicializados com os dados contidos neste arquivo
binário.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 50

typedef struct {
    char nome[MAX_NOME];
    char telefone[15];
    int diaAniversario;
    int mesAniversario;
} Contato;

void exibirMenu() {
    printf("========= Agenda de Contatos =========\n");
    printf("1. Inserir Contato\n");
    printf("2. Remover Contato\n");
    printf("3. Pesquisar Contato pelo Nome\n");
    printf("4. Listar Todos os Contatos\n");
    printf("5. Listar Contatos por Letra Inicial\n");
    printf("6. Imprimir Aniversariantes do Mês\n");
    printf("7. Sair\n");
    printf("======================================\n");
    printf("Escolha uma opção: ");
}

void inserirContato(Contato *agenda, int *numContatos) {
    if (*numContatos == 100) {
        printf("A agenda está cheia. Não é possível adicionar mais contatos.\n");
        return;
    }

    printf("Nome: ");
    scanf(" %[^\n]s", agenda[*numContatos].nome);

    printf("Telefone: ");
    scanf(" %[^\n]s", agenda[*numContatos].telefone);

    printf("Dia de Aniversário: ");
    scanf("%d", &agenda[*numContatos].diaAniversario);

    printf("Mês de Aniversário: ");
    scanf("%d", &agenda[*numContatos].mesAniversario);

    (*numContatos)++;
    printf("Contato adicionado com sucesso!\n");
}

void removerContato(Contato *agenda, int *numContatos) {
    char nome[MAX_NOME];
    printf("Digite o nome do contato a ser removido: ");
    scanf(" %[^\n]s", nome);

    int encontrado = 0;
    for (int i = 0; i < *numContatos; i++) {
        if (strcmp(agenda[i].nome, nome) == 0) {
            encontrado = 1;
            for (int j = i; j < *numContatos - 1; j++) {
                agenda[j] = agenda[j + 1];
            }
            (*numContatos)--;
            break;
        }
    }

    if (encontrado) {
        printf("Contato removido com sucesso!\n");
    } else {
        printf("Contato não encontrado.\n");
    }
}

void pesquisarContato(Contato *agenda, int numContatos) {
    char nome[MAX_NOME];
    printf("Digite o nome do contato a ser pesquisado: ");
    scanf(" %[^\n]s", nome);

    int encontrado = 0;
    for (int i = 0; i < numContatos; i++) {
        if (strcmp(agenda[i].nome, nome) == 0) {
            encontrado = 1;
            printf("Nome: %s\n", agenda[i].nome);
            printf("Telefone: %s\n", agenda[i].telefone);
            printf("Aniversário: %d/%d\n", agenda[i].diaAniversario, agenda[i].mesAniversario);
            printf("-------------------------\n");
            break;
        }
    }

    if (!encontrado) {
        printf("Contato não encontrado.\n");
    }
}

void listarContatos(Contato *agenda, int numContatos) {
    printf("Lista de Contatos:\n");

    for (int i = 0; i < numContatos; i++) {
        printf("Nome: %s\n", agenda[i].nome);
        printf("Telefone: %s\n", agenda[i].telefone);
        printf("Aniversário: %d/%d\n", agenda[i].diaAniversario, agenda[i].mesAniversario);
        printf("-------------------------\n");
    }
}

void listarContatosPorLetraInicial(Contato *agenda, int numContatos) {
    char letra;
    printf("Digite a letra inicial dos contatos a serem listados: ");
    scanf(" %c", &letra);

    printf("Contatos cujo nome inicia com '%c':\n", letra);

    for (int i = 0; i < numContatos; i++) {
        if (agenda[i].nome[0] == letra) {
            printf("Nome: %s\n", agenda[i].nome);
            printf("Telefone: %s\n", agenda[i].telefone);
            printf("Aniversário: %d/%d\n", agenda[i].diaAniversario, agenda[i].mesAniversario);
            printf("-------------------------\n");
        }
    }
}

void imprimirAniversariantesDoMes(Contato *agenda, int numContatos) {
    int mes;
    printf("Digite o mês dos aniversariantes a serem impressos: ");
    scanf("%d", &mes);

    printf("Aniversariantes do mês %d:\n", mes);

    for (int i = 0; i < numContatos; i++) {
        if (agenda[i].mesAniversario == mes) {
            printf("Nome: %s\n", agenda[i].nome);
            printf("Telefone: %s\n", agenda[i].telefone);
            printf("Aniversário: %d/%d\n", agenda[i].diaAniversario, agenda[i].mesAniversario);
            printf("-------------------------\n");
        }
    }
}

void salvarContatosEmArquivo(Contato *agenda, int numContatos) {
    FILE *arquivo = fopen("contatos.bin", "wb");

    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo.\n");
        return;
    }

    fwrite(&numContatos, sizeof(int), 1, arquivo);
    fwrite(agenda, sizeof(Contato), numContatos, arquivo);

    fclose(arquivo);
}

int main() {
    Contato agenda[100];
    int numContatos = 0;

    FILE *arquivo = fopen("contatos.bin", "rb");

    if (arquivo != NULL) {
        fread(&numContatos, sizeof(int), 1, arquivo);
        fread(agenda, sizeof(Contato), numContatos, arquivo);

        fclose(arquivo);
    }

    int opcao;
    do {
        exibirMenu();
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                inserirContato(agenda, &numContatos);
                break;
            case 2:
                removerContato(agenda, &numContatos);
                break;
            case 3:
                pesquisarContato(agenda, numContatos);
                break;
            case 4:
                listarContatos(agenda, numContatos);
                break;
            case 5:
                listarContatosPorLetraInicial(agenda, numContatos);
                break;
            case 6:
                imprimirAniversariantesDoMes(agenda, numContatos);
                break;
            case 7:
                salvarContatosEmArquivo(agenda, numContatos);
                printf("Encerrando o programa...\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
                break;
        }
    } while (opcao != 7);

    return 0;
}
---------------------------------------------------------------------
26.Crie um programa que declare uma estrutura para o cadastro de alunos.
a) Dever ao ser armazenados, para cada aluno: matrícula, sobrenome
(apenas um), e ano de nascimento;
b) Ao início do programa, o usuário deverá informar o número de alunos
que serão armazenados;
c) O programa deverá alocar dinamicamente a quantidade necessária
de memória para armazenar os registros dos alunos;
d) O programa deverá pedir ao usuário que entre com as informações
dos alunos;
e) Em seguida, essas informações dever ˜ao ser gravadas em um
arquivo;
f) Ao fnal, mostrar os dados armazenados e liberar a memória alocada.
Ao iniciar o programa, forneça ao usuário uma opção para carregar os
registros do arquivo para a memória do computador alocando
dinamicamente a quantidade de memória necessária.
Dica: para que o usuário possa entrar com novos dados, além dos que
foram obtidos a partir do arquivo, use a função realloc() para realocar a
quantidade de memória usada.
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int matricula;
    char sobrenome[100];
    int anoNascimento;
} Aluno;

void carregarRegistros(Aluno **alunos, int *numAlunos) {
    FILE *arquivo = fopen("alunos.dat", "rb");
    if (arquivo == NULL) {
        printf("Arquivo não encontrado.\n");
        return;
    }

    fread(numAlunos, sizeof(int), 1, arquivo);

    *alunos = (Aluno *)realloc(*alunos, (*numAlunos) * sizeof(Aluno));

    fread(*alunos, sizeof(Aluno), *numAlunos, arquivo);

    fclose(arquivo);

    printf("Registros carregados com sucesso.\n");
}

void gravarRegistros(Aluno *alunos, int numAlunos) {
    FILE *arquivo = fopen("alunos.dat", "wb");
    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return;
    }

    fwrite(&numAlunos, sizeof(int), 1, arquivo);
    fwrite(alunos, sizeof(Aluno), numAlunos, arquivo);

    fclose(arquivo);

    printf("Registros gravados com sucesso.\n");
}

void cadastrarAluno(Aluno **alunos, int *numAlunos) {
    *alunos = (Aluno *)realloc(*alunos, (*numAlunos + 1) * sizeof(Aluno));

    printf("Matrícula: ");
    scanf("%d", &(*alunos)[*numAlunos].matricula);

    printf("Sobrenome: ");
    scanf(" %[^\n]s", (*alunos)[*numAlunos].sobrenome);

    printf("Ano de Nascimento: ");
    scanf("%d", &(*alunos)[*numAlunos].anoNascimento);

    (*numAlunos)++;

    printf("Aluno cadastrado com sucesso.\n");
}

void exibirAlunos(Aluno *alunos, int numAlunos) {
    printf("----- Alunos Cadastrados -----\n");
    for (int i = 0; i < numAlunos; i++) {
        printf("Matrícula: %d\n", alunos[i].matricula);
        printf("Sobrenome: %s\n", alunos[i].sobrenome);
        printf("Ano de Nascimento: %d\n", alunos[i].anoNascimento);
        printf("-----------------------------\n");
    }
}

void liberarMemoria(Aluno *alunos) {
    free(alunos);
    printf("Memória liberada.\n");
}

int main() {
    Aluno *alunos = NULL;
    int numAlunos = 0;
    int opcao;

    printf("Informe o número de alunos a serem cadastrados: ");
    scanf("%d", &numAlunos);

    alunos = (Aluno *)malloc(numAlunos * sizeof(Aluno));

    do {
        printf("----- Menu -----\n");
        printf("1. Cadastrar Aluno\n");
        printf("2. Exibir Alunos\n");
        printf("3. Gravar Registros\n");
        printf("4. Carregar Registros\n");
        printf("5. Liberar Memória\n");
        printf("6. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                cadastrarAluno(&alunos, &numAlunos);
                break;
            case 2:
                exibirAlunos(alunos, numAlunos);
                break;
            case 3:
                gravarRegistros(alunos, numAlunos);
                break;
            case 4:
                carregarRegistros(&alunos, &numAlunos);
                break;
            case 5:
                liberarMemoria(alunos);
                break;
            case 6:
                printf("Encerrando o programa...\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
                break;
        }
    } while (opcao != 6);

    return 0;
}
-----------------------------------------------------------------------
27.Faça um programa para gerenciar as notas dos alunos de uma turma
salva em um arquivo. O programa deverá ter um menu contendo as
seguintes opções:
 Defnir informações da turma;
 Inserir aluno e notas;
 Exibir alunos e médias;
 Exibir alunos aprovados;
 Exibir alunos reprovados;
 Salvar dados em Disco;
 Sair do programa (fm).
Faça a rotina que gerencia o menu dentro do main, e para cada uma das
opções deste menu, crie uma função específca.
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    char nome[100];
    float nota1;
    float nota2;
    float media;
} Aluno;

Aluno *alunos;
int numAlunos;
int turmaDefinida = 0;

void definirInformacoesTurma() {
    printf("Informe o número de alunos da turma: ");
    scanf("%d", &numAlunos);

    alunos = (Aluno *)malloc(numAlunos * sizeof(Aluno));

    for (int i = 0; i < numAlunos; i++) {
        printf("Nome do aluno %d: ", i + 1);
        scanf(" %[^\n]s", alunos[i].nome);
    }

    turmaDefinida = 1;

    printf("Informações da turma definidas.\n");
}

void inserirAlunoNotas() {
    if (!turmaDefinida) {
        printf("Defina as informações da turma antes de inserir as notas dos alunos.\n");
        return;
    }

    char nomeAluno[100];
    int encontrado = 0;

    printf("Nome do aluno: ");
    scanf(" %[^\n]s", nomeAluno);

    for (int i = 0; i < numAlunos; i++) {
        if (strcmp(alunos[i].nome, nomeAluno) == 0) {
            printf("Nota 1: ");
            scanf("%f", &alunos[i].nota1);

            printf("Nota 2: ");
            scanf("%f", &alunos[i].nota2);

            alunos[i].media = (alunos[i].nota1 + alunos[i].nota2) / 2;

            encontrado = 1;
            break;
        }
    }

    if (!encontrado) {
        printf("Aluno não encontrado.\n");
    } else {
        printf("Notas inseridas com sucesso.\n");
    }
}

void exibirAlunosMedias() {
    if (!turmaDefinida) {
        printf("Defina as informações da turma antes de exibir as médias dos alunos.\n");
        return;
    }

    printf("----- Alunos e Médias -----\n");
    for (int i = 0; i < numAlunos; i++) {
        printf("Aluno: %s\n", alunos[i].nome);
        printf("Média: %.2f\n", alunos[i].media);
        printf("--------------------------\n");
    }
}

void exibirAlunosAprovados() {
    if (!turmaDefinida) {
        printf("Defina as informações da turma antes de exibir os alunos aprovados.\n");
        return;
    }

    printf("----- Alunos Aprovados -----\n");
    for (int i = 0; i < numAlunos; i++) {
        if (alunos[i].media >= 6.0) {
            printf("Aluno: %s\n", alunos[i].nome);
            printf("Média: %.2f\n", alunos[i].media);
            printf("--------------------------\n");
        }
    }
}

void exibirAlunosReprovados() {
    if (!turmaDefinida) {
        printf("Defina as informações da turma antes de exibir os alunos reprovados.\n");
        return;
    }

    printf("----- Alunos Reprovados -----\n");
    for (int i = 0; i < numAlunos; i++) {
        if (alunos[i].media < 6.0) {
            printf("Aluno: %s\n", alunos[i].nome);
            printf("Média: %.2f\n", alunos[i].media);
            printf("--------------------------\n");
        }
    }
}

void salvarDadosEmDisco() {
    if (!turmaDefinida) {
        printf("Defina as informações da turma antes de salvar os dados em disco.\n");
        return;
    }

    FILE *arquivo = fopen("notas.dat", "wb");
    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo.\n");
        return;
    }

    fwrite(&numAlunos, sizeof(int), 1, arquivo);
    fwrite(alunos, sizeof(Aluno), numAlunos, arquivo);

    fclose(arquivo);

    printf("Dados salvos em disco com sucesso.\n");
}

void sairDoPrograma() {
    free(alunos);
    printf("Encerrando o programa...\n");
}

int main() {
    int opcao;

    do {
        printf("----- Menu -----\n");
        printf("1. Definir Informações da Turma\n");
        printf("2. Inserir Aluno e Notas\n");
        printf("3. Exibir Alunos e Médias\n");
        printf("4. Exibir Alunos Aprovados\n");
        printf("5. Exibir Alunos Reprovados\n");
        printf("6. Salvar Dados em Disco\n");
        printf("7. Sair do Programa\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                definirInformacoesTurma();
                break;
            case 2:
                inserirAlunoNotas();
                break;
            case 3:
                exibirAlunosMedias();
                break;
            case 4:
                exibirAlunosAprovados();
                break;
            case 5:
                exibirAlunosReprovados();
                break;
            case 6:
                salvarDadosEmDisco();
                break;
            case 7:
                sairDoPrograma();
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
                break;
        }
    } while (opcao != 7);

    return 0;
}
--------------------------------------------------------------------------------
28.Faça um programa que recebe como entrada o nome de um arquivo de
entrada e o nome de um arquivo de saída. Cada linha do arquivo de
entrada possui colunas de tamanho de 30 caracteres. No arquivo de
saída deverá ser escrito o arquivo de entrada de forma inversa. Veja um
exemplo:
Arquivo de entrada:
Hoje eh dia de prova de PP
A prova esta muito facil
Vou tirar uma boa nota
Arquivo de saida:
Aton aob amu rarit uov
Licaf otium atse avorp A
PP ed avorp ed aid he ejoH
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CHARACTERS 30

void inverterLinha(char linha[]) {
    int tamanho = strlen(linha);
    char temp;

    for (int i = 0, j = tamanho - 1; i < j; i++, j--) {
        temp = linha[i];
        linha[i] = linha[j];
        linha[j] = temp;
    }
}

int main() {
    char nomeArquivoEntrada[100];
    char nomeArquivoSaida[100];

    printf("Digite o nome do arquivo de entrada: ");
    scanf("%s", nomeArquivoEntrada);

    printf("Digite o nome do arquivo de saída: ");
    scanf("%s", nomeArquivoSaida);

    FILE *arquivoEntrada = fopen(nomeArquivoEntrada, "r");
    FILE *arquivoSaida = fopen(nomeArquivoSaida, "w");

    if (arquivoEntrada == NULL || arquivoSaida == NULL) {
        printf("Erro ao abrir os arquivos.\n");
        return 1;
    }

    char linha[MAX_CHARACTERS + 1];

    while (fgets(linha, sizeof(linha), arquivoEntrada) != NULL) {
        inverterLinha(linha);
        fputs(linha, arquivoSaida);
    }

    fclose(arquivoEntrada);
    fclose(arquivoSaida);

    printf("Arquivo de saída gerado com sucesso.\n");

    return 0;
}
--------------------------------------------------
29.Codifque um programa que manipule um arquivo contendo registros
descritos pelos seguintes campos: codigo_vendedor, nome_vendedor,
valor_da_venda e mes. A manipulação do arquivo em questão é feita
através da execução das operações disponibilizadas pelo seguinte menu:
 Criar o arquivo de dados;
 Incluir um determinado registro no arquivo;
 Excluir um determinado vendedor no arquivo;
 Alterar o valor de uma venda no arquivo;
 Imprimir os registros na saída padrão;
 Excluir o arquivo de dados;
 Finalizar o programa.
Os registros devem estar ordenados no arquivo, de forma crescente, de
acordo com as Informações contidas nos campos código vendedor e mês.
Não deve existir mais de um registro no arquivo com mesmos valores nos
campos código vendedor e mês.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NOME 50

struct Registro {
    int codigo_vendedor;
    char nome_vendedor[MAX_NOME];
    float valor_da_venda;
    int mes;
};

void criarArquivo() {
    FILE *arquivo = fopen("dados.txt", "wb");
    if (arquivo == NULL) {
        printf("Erro ao criar o arquivo de dados.\n");
        return;
    }
    fclose(arquivo);
    printf("Arquivo de dados criado com sucesso.\n");
}

void incluirRegistro() {
    struct Registro registro;

    printf("Digite o código do vendedor: ");
    scanf("%d", &registro.codigo_vendedor);

    printf("Digite o nome do vendedor: ");
    scanf(" %[^\n]", registro.nome_vendedor);

    printf("Digite o valor da venda: ");
    scanf("%f", &registro.valor_da_venda);

    printf("Digite o mês: ");
    scanf("%d", &registro.mes);

    FILE *arquivo = fopen("dados.txt", "ab");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo de dados.\n");
        return;
    }
    fwrite(&registro, sizeof(struct Registro), 1, arquivo);
    fclose(arquivo);
    printf("Registro incluído com sucesso.\n");
}

void excluirRegistro() {
    int codigo, mes;
    printf("Digite o código do vendedor a ser excluído: ");
    scanf("%d", &codigo);

    printf("Digite o mês do registro a ser excluído: ");
    scanf("%d", &mes);

    FILE *arquivo = fopen("dados.txt", "r+b");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo de dados.\n");
        return;
    }

    struct Registro registro;
    int encontrado = 0;

    while (fread(&registro, sizeof(struct Registro), 1, arquivo) == 1) {
        if (registro.codigo_vendedor == codigo && registro.mes == mes) {
            encontrado = 1;
            break;
        }
    }

    if (encontrado) {
        // Move o cursor para a posição anterior ao registro encontrado
        fseek(arquivo, -sizeof(struct Registro), SEEK_CUR);
        // Sobrescreve o registro com 0 bytes, marcando-o como excluído
        fwrite(&registro, sizeof(struct Registro), 1, arquivo);
        printf("Registro excluído com sucesso.\n");
    } else {
        printf("Registro não encontrado.\n");
    }

    fclose(arquivo);
}

void alterarValorVenda() {
    int codigo, mes;
    float novo_valor;

    printf("Digite o código do vendedor: ");
    scanf("%d", &codigo);

    printf("Digite o mês do registro: ");
    scanf("%d", &mes);

    printf("Digite o novo valor da venda: ");
    scanf("%f", &novo_valor);

    FILE *arquivo = fopen("dados.txt", "r+b");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo de dados.\n");
        return;
    }

    struct Registro registro;
    int encontrado = 0;

    while (fread(&registro, sizeof(struct Registro), 1, arquivo) == 1) {
        if (registro.codigo_vendedor == codigo && registro.mes == mes) {
            encontrado = 1;
            break;
        }
    }

    if (encontrado) {
        // Move o cursor para a posição anterior ao registro encontrado
        fseek(arquivo, -sizeof(struct Registro), SEEK_CUR);
        // Atualiza o valor da venda
        registro.valor_da_venda = novo_valor;
        // Sobrescreve o registro com as novas informações
        fwrite(&registro, sizeof(struct Registro), 1, arquivo);
        printf("Valor da venda alterado com sucesso.\n");
    } else {
        printf("Registro não encontrado.\n");
    }

    fclose(arquivo);
}

void imprimirRegistros() {
    FILE *arquivo = fopen("dados.txt", "rb");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo de dados.\n");
        return;
    }

    struct Registro registro;

    while (fread(&registro, sizeof(struct Registro), 1, arquivo) == 1) {
        printf("Código do vendedor: %d\n", registro.codigo_vendedor);
        printf("Nome do vendedor: %s\n", registro.nome_vendedor);
        printf("Valor da venda: %.2f\n", registro.valor_da_venda);
        printf("Mês: %d\n", registro.mes);
        printf("----------------------------\n");
    }

    fclose(arquivo);
}

void excluirArquivo() {
    int confirmacao;
    printf("Tem certeza que deseja excluir o arquivo de dados? (1-Sim / 0-Não): ");
    scanf("%d", &confirmacao);

    if (confirmacao == 1) {
        if (remove("dados.txt") == 0) {
            printf("Arquivo de dados excluído com sucesso.\n");
        } else {
            printf("Erro ao excluir o arquivo de dados.\n");
        }
    }
}

int main() {
    int opcao;
    do {
        printf("Menu de Opções\n");
        printf("1. Criar o arquivo de dados\n");
        printf("2. Incluir um registro\n");
        printf("3. Excluir um vendedor\n");
        printf("4. Alterar o valor de uma venda\n");
        printf("5. Imprimir os registros\n");
        printf("6. Excluir o arquivo de dados\n");
        printf("7. Finalizar o programa\n");
        printf("Digite a opção desejada: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                criarArquivo();
                break;
            case 2:
                incluirRegistro();
                break;
            case 3:
                excluirRegistro();
                break;
            case 4:
                alterarValorVenda();
                break;
            case 5:
                imprimirRegistros();
                break;
            case 6:
                excluirArquivo();
                break;
            case 7:
                printf("Programa finalizado.\n");
                break;
            default:
                printf("Opção inválida.\n");
        }
    } while (opcao != 7);

    return 0;
}
