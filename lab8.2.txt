/*1 Crie um programa que contenha um array de ﬂoat contendo 10 elementos.
Utilizando aritmética de ponteiro, imprima o endereço de cada posição
desse array*/
#include<stdio.h>
#include<stdlib.h>

int main (){

    //Declarando Variáveis
    float vet[10] ={1, 2.5, 3, 5.6, 5, 6.6, 7, 8.8, 9, 12.5}; 
    int i; 

    //Declarando Ponteiros
    float *p; 

    //Apontando os ponteiros para as variáveis declaradas
    p = vet; 
    

    //Imprimindo o endereço de cada posição

    for (i=0; i<10; i++){
     printf("\n O valor %.1f tem como endereco : %p", *(p+i), (p+i));
    }
   

return 0; 
}
-------------------------------------------------------------------
/*2 Crie um programa que contenha uma matriz de ﬂoat contendo 3 linhas e 3
colunas. Utilizando aritmética de ponteiro, imprima o endereço de cada
posição dessa matriz.*/
#include<stdio.h>
#include<stdlib.h>

int main (){

    //Declarando Variáveis
    float mat[3][3]={{1.6,2,5.7},{8.3,3,2.6},{7.5, 5, 4}}; 
    int i; 

    //Declarando Ponteiros
    float *p; 
    
    p = &mat[0][0];

    //Imprimindo o endereço de cada posição
    for (i=0; i<9; i++){
            printf("\n O valor %.1f tem como endereco : %p", *(p+i), (p+i));
    }
   
return 0;  
}
-------------------------------------------------------------------------
/*3 Crie um programa que contenha um array de inteiros contendo 5 elementos.
Utilizando apenas aritmética de ponteiros, leia esse array do teclado e
imprima o dobro de cada valor lido.*/
#include<stdio.h>
#include<stdlib.h>

int main (){

    //Declarando Variáveis
    int vet[5]; 
    int i; 

    //Declarando Ponteiros
    int *p; 

    //Lendo valores 
    for(i=0; i<5; i++){
        printf("\nInforme o numero:"); 
        scanf("%d", &vet[i]); 
    }

    p = vet;

    //Imprimindo o dobro de cada valor lido 
    for(i=0; i<5; i++){
        printf("\nO dobro de %d eh %d", *(p+i), (*(p+i)*2));
    }
return 0;  
}
----------------------------------------------------------------
/*4 Crie um programa que contenha um array contendo 5 elementos inteiros.
Leia esse array do teclado e imprima o endereço das posições contendo
valores pares*/

#include<stdio.h>
#include<stdlib.h>

int main (){

    //Declarando Variáveis
    int vet[5]; 
    int i; 

    //Declarando Ponteiros
    int *p; 
    p = vet;

    //Lendo valores 
    for(i=0; i<5; i++){
        printf("\nInforme o numero:"); 
        scanf("%d", (p+i)); 
    }
    
    //Imprimindo o endereço das posições contendo valores pares 
    for(i=0; i<5; i++){
        if((*(p+i)%2) == 0){
            printf("\nO numero %d eh par e seu endereco eh %p", *(p+i), (p+i));

        } 
    }
return 0;  
}
-------------------------------------------------------------------------------
/*5 Elabore um programa que receba duas strings digitadas pelo usuário e
verifque se a segunda string ocorre dentro da primeira. Use aritmética de
ponteiros para acessar os caracteres das strings*/

#include <stdio.h>

int stringContains(const char *str1, const char *str2) {
    while (*str1) {
        const char *temp1 = str1;
        const char *temp2 = str2;

        // Verifica se os caracteres das duas strings são iguais
        while (*temp1 && *temp2 && (*temp1 == *temp2)) {
            temp1++;
            temp2++;
        }

        // Se a segunda string foi completamente percorrida, significa que ela ocorre dentro da primeira
        if (!*temp2) {
            return 1;
        }

        str1++;
    }

    return 0;
}

int main() {
    char str1[100];
    char str2[100];

    printf("Digite a primeira string: ");
    scanf("%s", str1);

    printf("Digite a segunda string: ");
    scanf("%s", str2);

    // Chama a função para verificar se a segunda string ocorre dentro da primeira
    if (stringContains(str1, str2)) {
        printf("A segunda string ocorre dentro da primeira.\n");
    } else {
        printf("A segunda string nao ocorre dentro da primeira.\n");
    }

    return 0;
}

------------------------------------------------------------------------------
/*6 Elabore um programa que dado um array e um valor do mesmo tipo do
array, preencha os elementos de array com esse valor. Não utilize índices
para percorrer o array, apenas aritmética de ponteiros*/
#include <stdio.h>

void fillArray(int *array, int size, int value) {
    // Percorre o array utilizando aritmética de ponteiros e preenche os elementos com o valor especificado
    for (int i = 0; i < size; i++) {
        *(array + i) = value;
    }
}

int main() {
    int array[5];
    int value;

    printf("Digite o valor para preencher o array: ");
    scanf("%d", &value);

    // Chama a função para preencher o array com o valor especificado
    fillArray(array, 5, value);

    printf("Array preenchido:\n");
    for (int i = 0; i < 5; i++) {
        printf("%d ", *(array + i));
    }
    printf("\n");

    return 0;
}
----------------------------------------------------------------------------
/*7 Escreva um programa que receba um array de inteiros com 10 elementos
digitados pelo usuário e encontre o menor (min) e o maior (max) elemento
desse array. Utilize ponteiros tanto para acessar o array quanto para acessar
as variáveis min e max, ou seja, são necessários pelo menos 3 ponteiros.*/
#include <stdio.h>
#include<stdlib.h> 

void findMinMax(int *array, int size, int *min, int *max) {
    // Inicializa min e max com o primeiro elemento do array
    *min = *max = *array;

    // Percorre o array e atualiza min e max conforme necessário
    for (int i = 1; i < size; i++) {
        if (*(array + i) < *min) {
            *min = *(array + i);
        }
        if (*(array + i) > *max) {
            *max = *(array + i);
        }
    }
}

int main() {
    int array[10];
    int min, max;

    printf("Digite 10 numeros inteiros:\n");

    // Lê os valores digitados pelo usuário e armazena no array
    for (int i = 0; i < 10; i++) {
        scanf("%d", &array[i]);
    }

    // Chama a função para encontrar o menor e o maior elemento
    findMinMax(array, 10, &min, &max);

    printf("O menor elemento eh: %d\n", min);
    printf("O maior elemento eh: %d\n", max);

    return 0;
}

------------------------------------------------------------------------------
/* 8 Considere a seguinte declaração: int A, *B, **C, ***D; Escreva um
programa que leia a variável ‘A’ e calcule e exiba o dobro, o triplo e o
quádruplo desse valor utilizando apenas os ponteiros B, C e D. O ponteiro B
deve ser usada para calcular o dobro, C o triplo e D o quádruplo.*/ 
#include <stdio.h>
#include <stdlib.h> 

int main() {
	int a;
	int *b = &a;
	int **c = &b;
	int ***d = &c;
	
	printf("\nDigite o valor base: ");
	scanf("%d", &a);
	
	printf("\nDobro: %d", (*b * 2));
	printf("\nTriplo: %d", (**c * 3));
	printf("\nQuadruplo: %d", (***d * 4)); 
	
	return 0;
}
