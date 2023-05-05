#include <stdio.h>
#include <stdlib.h>

int main()
{

    char nome[100];
    char i, j;

    printf("Digite: ");
    fgets(nome, 100, stdin);

    for(i=0; i<100; i++){
            if(nome[i]=='r'&& nome[i+1]==' '){
                continue;
            }
            else if (nome[i]=='r'&& nome[i+1]=='r'){
                nome [i] = 'l';

                for(j=i+1; j<100; j++){
                    nome[j] = nome[j+1];
                }
            } else if(nome[i]=='r'){
                nome[i]='l';
            }
    }

    printf("\nA troca fica %s", nome);



    return 0;
}

