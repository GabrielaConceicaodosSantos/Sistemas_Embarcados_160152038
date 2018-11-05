
GABRIELA CONCEIÇÃO DOS SANTOS. 16/0152038 - 2.2018



1. Crie um programa em C que cria uma thread, e faça com que o programa principal envie os valores 1, 2, 3, 4, 5, 6, 7, 8, 9 e 10 para a thread, com intervalos de 1 segundo entre cada envio. Depois de o programa principal enviar o número 10, ele aguarda 1 segundo e termina a execução. A thread escreve na tela cada valor recebido, e quando ela receber o valor 10, ela termina a execução.

RESPOSTA:

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

int var_comunicacao;

void* funcao_thread( void* inutil){

	int i;
	int valores_principal[10];

	for( i = 0; i < 10; i++){
		sleep(0.1);
		valores_principal[i] = var_comunicacao;
		sleep(1);
	}

	for( i = 0; i < 10; i++){
		printf(" %d, ",valores_principal[i]);
	}
	printf("\n");
	return NULL;
}

int main(int argc, char** argv){
	
	int i;
	pthread_t thread_ID;
	pthread_create(&thread_ID, NULL, &funcao_thread, NULL);
	for(i = 0; i <10; i++){
		var_comunicacao = i+1;
		sleep(1);
	}
	sleep(1);
	return 0;
}


2. Crie um programa em C que preenche o vetor long int v[50000] completamente com valores aleatórios (use a função random()), e que procura o valor máximo do vetor por dois métodos:
(a) Pela busca completa no vetor v[];

RESPOSTA:

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

long int v[50000];

long int encontra_maior(long int* vetor){

	long int maior = vetor[0];
	for( int i = 1; i <50000; i++){
		if(vetor[i] > maior)
			maior = vetor[i];
	}
	return maior;
}


int main(int argc, char** argv){
	
	int i;
	long int valor_maior;
	for(i = 0; i <50000; i++){
		v[i] = random();
	}
	valor_maior = encontra_maior(v);
	printf("Número maior: %d\n", valor_maior);
	return 0;
}
(b) Separando o vetor em 4 partes, e usando 4 threads para cada uma encontrar o máximo de cada parte. Ao final das threads, o programa principal compara o resultado das quatro threads para definir o máximo do vetor.

RESPOSTA:

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

long int v[50000];
long int v1[12500];
long int v2[12500];
long int v3[12500];
long int v4[12500];
long int maiores[4];

long int encontra_maior(long int* vetor, int N){

	long int maior = vetor[0];
	for( int i = 1; i < N; i++){
		if(vetor[i] > maior){
			maior = vetor[i];
			}
	}
	return maior;

}

void* thread1( void* inutil){
	maiores[0] = encontra_maior(v1, 12500);
	return NULL;
}

void* thread2( void* inutil){
	maiores[1] = encontra_maior(v2, 12500);
	return NULL;
}

void* thread3( void* inutil){
	maiores[2] = encontra_maior(v3, 12500);
	return NULL;
}

void* thread4( void* inutil){
	maiores[3] = encontra_maior(v4, 12500);
	return NULL;
}


int main(int argc, char** argv){
	
	int i;

	pthread_t thread_id1, thread_id2, thread_id3, thread_id4;

	long int valor_maior;
	for(i = 0; i <50000; i++){
		v[i] = random();
	}
	for(i = 0; i <12500; i++){
		v1[i] = v[i];
		v2[i] = v[12500+i];
		v3[i] = v[25000+i];
		v4[i] = v[37500+i];
	}

	pthread_create(&thread_id1, NULL, &thread1, NULL);
	pthread_create(&thread_id2, NULL, &thread2, NULL);
	pthread_create(&thread_id3, NULL, &thread3, NULL);
	pthread_create(&thread_id4, NULL, &thread4, NULL);	

	pthread_join(thread_id1,NULL);
	pthread_join(thread_id2,NULL);
	pthread_join(thread_id3,NULL);
	pthread_join(thread_id4,NULL);	
	
	valor_maior = encontra_maior(maiores,4);

	printf("Número maior: %d\n", valor_maior);
	return 0;
}
Ao final do programa principal, compare os resultados obtidos pelos dois métodos.

Ambos tiveram como resposta final o valor de 2147469841. Esperasse que o metodo da letra b seja mais rápido que o da letra a, porém não é notado devido a velocidade do processador.



3. Repita o exercício anterior, mas calcule a média do vetor ao invés do valor máximo.

4. Repita o exercício anterior, mas calcule a variância do vetor ao invés da média.
