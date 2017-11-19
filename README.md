//a seguir está um modelo de implementação com utilização de includes reconhecíveis via compilador C/C++, por ex. DEV c++, sublime,Codeblocks,C++ da Borland,etc.
//a seguir vai o exemplo da versão , relativa ao executável,a interface difere apenas no executável da versão mais estática
//

//Essa versão corresponde a um cadastramento utilizando modelos de struct /union, esse é um exemplo do arquivo .c de código fonte de um dos  modelos executáveis
exemplo do .h:
typedef struct {
        char nome [30];
        int numero;
        int tel;
        short usado;
                       
        } Aluno;


typedef struct {
         char titulo [30];
         int isbn;
         int ncopias;
         short usado;
        } Livro;


typedef struct {
int isbn;
int nrusp;
short usado;
}Fila;

typedef struct {
int isbn;
int nrusp;
short usado;
}ListaEmprestimo;

void iniciaLivro (Livro vet2[]) ;
void iniciaFila(Fila vetFila[]);
void iniciaListaEmprestimo (ListaEmprestimo vetLista[]);
void cadastraAluno (Aluno *a);
void cadastraLivro (Livro *l);
void cadastraFila (Fila *F,int isbn,int nrusp);
void cadastraListaEmprestimo (ListaEmprestimo *L,int isbn,int nrusp);
int insereCadAluno (Aluno vet[],Aluno a);
int insereCadLivro (Livro vet2[],Livro l);
int insereListaEmprestimo(ListaEmprestimo vetLista[],ListaEmprestimo L);
int insereFila(Fila vetFila[],Fila F);
void imprimeAluno (Aluno vet[]);
void imprimeLivro (Livro vet2[]);
void imprimeFila (Fila vetFila[],int isbn);
void imprimeLista (ListaEmprestimo vetLista[],int isbn); 
void imprimeListaAluno (ListaEmprestimo vetLista[],int nro);
int checaFila (Fila vetFila[],int isbn);
void retiraLista (ListaEmprestimo vetLista[],int isbn,int nrusp);
void retiraFila (Fila vetFila[],int isbn,int nrusp);
int buscaLivroCod (Livro vet2[], int isbn);
int buscaAlunoCod (Aluno vet[], int nrusp);
int imprimeBuscaLivro (Livro vet2[], int j);
int emprestaLivro (Livro vet2[], int isbn,int nrusp);
int retornaLivro (Livro vet2[], int isbn,int nrusp);



///////////////////////////////////////////////////////////////////////////////////////////////////////
E aqui um exemplo de main.c
//





#include <stdlib.h>
#include <stdio.h>
#include "DinamicTAD.h"



void cadastraAluno (elem *a) {
      printf ("Nome:");
      scanf ("%s", (*a).Aluno.nome);
      printf ("email:");
      scanf ("%s", (*a).Aluno.email);
      printf ("Numero:");
      scanf ("%d", &(*a).Aluno.nrusp);
      printf ("Tel:");
      scanf ("%d", &(*a).Aluno.tel);
      fflush (stdin);
      }
void cadastraLivro (elem *a) {
      printf ("Titulo:");
      scanf ("%s", (*a).Livro.titulo);
      printf ("Autor:");
      scanf ("%s",(*a).Livro.autor);
      printf ("ISBN:");
      scanf ("%d",&(*a).Livro.isbn);
      printf ("Editora:");
      scanf ("%s", (*a).Livro.editora);
      printf ("Ano:");
      scanf ("%d", &(*a).Livro.ano);
      printf ("Edicao:");
      scanf ("%d", &(*a).Livro.edicao);
      printf ("Numero de copias:");
      scanf ("%d", &(*a).Livro.ncopias);  
      fflush (stdin);
      }

void cria(Banco *L){
	L->inicio = NULL;
	L->fim = NULL;
    
}

void inserir(Banco *L, elem *X, int *erro){
	
	no *p;
	
	p = (no*)malloc(sizeof(no));
	if(p==NULL){
		*erro = 1;
		return;
	} else *erro = 0;
	
	p->info = *X;
	p->prox = NULL;
	
	if(L->inicio == NULL)
		L->inicio = p;
		else L->fim->prox = p;
		
	L->fim = p;
	
}



int retiraLivro(Banco *L,int isbn){
	
	no *p;
	p=L->inicio;
	
	while((p != NULL)&&(p->info.Livro.isbn != isbn)){
		p=p->prox;
	}
	
	if(p==NULL)
		return 0;
		else 
        p->info.Livro.ncopias --;
        return  p->info.Livro.ncopias;
	
}
 
int retornaLivro(Banco *L,int isbn){
	
	no *p;
	p=L->inicio;
	
	while((p != NULL)&&(p->info.Livro.isbn != isbn)){
		p=p->prox;
	}
	
	if(p==NULL)
		return 0;
		else 
        p->info.Livro.ncopias ++;
        return  p->info.Livro.ncopias;
	
}

void DeletaLivro(Banco *L,int isbn, int *erro){
	no* anterior,*atual,*p;

	if(atual == NULL)
		*erro = 1;
	else if(atual->info.Livro.isbn == p->info.Livro.isbn ){
		if(atual == L->inicio){
			L->inicio = L->inicio->prox;
			if(L->inicio == NULL)
				L->fim = NULL;
		} else if(atual == L->fim){
			L->fim = anterior;
			L->fim->prox = NULL;		
		} else anterior->prox = atual->prox;
		free(atual);
		*erro = 0;
	}else DeletaLivro(L,isbn ,erro);
	
}

void DeletaAluno(Banco *L,int nrusp, int *erro){
	no* anterior,*atual,*p;

	if(atual == NULL)
		*erro = 1;
	else if(atual->info.Aluno.nrusp == p->info.Aluno.nrusp ){
		if(atual == L->inicio){
			L->inicio = L->inicio->prox;
			if(L->inicio == NULL)
				L->fim = NULL;
		} else if(atual == L->fim){
			L->fim = anterior;
			L->fim->prox = NULL;		
		} else anterior->prox = atual->prox;
		free(atual);
		*erro = 0;
	}else DeletaLivro(L,nrusp ,erro);
	
}

int imprimeLivro(Banco *L,int isbn){
	
	no *p;
	p=L->inicio;
	
	while((p != NULL)&&(p->info.Livro.isbn != isbn)){
		p=p->prox;
	}
	
	if(p==NULL)
		return 0;
		else 
        printf ("%s \n",p->info.Livro.titulo);
        printf ("%d copias \n",p->info.Livro.ncopias);
        return  1;
	
}






