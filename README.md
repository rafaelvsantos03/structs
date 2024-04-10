#include <stdlib.h>
#include <stdio.h>

typedef struct carro{
    char modelo[20];
    char marca[20];
    int ano;
    int potencia;
    float valor;
}TipoCarro;

TipoCarro *aloca(int tam);
void alterar(TipoCarro *pcarro, int tam);
void desaloca(TipoCarro **pcarro);
void imprimir(TipoCarro *pcarro, int tam);

int main()
{    
    TipoCarro *p;
    int tam;
    int x;
    printf("Informe a quantidade de carros:\n");
    scanf("%d",&tam);
    p=aloca(tam);
    alterar(p,tam);
    //printf("\nCarro %s inserido",p->modelo);
    //printf("\nQual carro deseja  ver as informacoes?\n");
    //scanf("%d",&x);
    printf("Imprimindo todos\n============================\n");
    imprimir(p,tam);
    desaloca(&p);
}
TipoCarro *aloca(int tam)
{
    TipoCarro *novo=NULL;
    novo = (TipoCarro *) malloc(sizeof(TipoCarro)*tam);
    if(novo == NULL) return NULL;
    return novo;
}

void alterar(TipoCarro *pcarro, int tam)
{
    int i;
    if(pcarro==NULL)
    {
        printf("\nNao houve alocacao!\n");
        return;
    }
    for(i=0;i<tam;i++)
    {
        setbuf(stdin,NULL);  //limpa o buffer do teclado
        printf("\nInforme o modelo: ");
        fgets((pcarro+i)->modelo,20,stdin);
        setbuf(stdin,NULL);
        printf("\nInforme a marca: ");
        fgets((pcarro+i)->marca,20,stdin);
        setbuf(stdin,NULL);
        printf("\nInforme o ano: ");
        scanf("%d",&((pcarro+i)->ano));
        setbuf(stdin,NULL);
        printf("\nInforme a potencia: ");
        scanf("%d",&((pcarro+i)->potencia));
        setbuf(stdin,NULL);
        printf("\nInforme o valor: ");
        scanf("%f",&((pcarro+i)->valor));
    }
}

void imprimir(TipoCarro *pcarro, int tam)
{
    int i;
    for(i=0;i<tam;i++)
    {
        printf("\nMarca:%s",(pcarro+i)->marca);
        printf("\nModelo: %s",(pcarro+i)->modelo);
        printf("\nAno: %d",(pcarro+i)->ano);
        printf("\nPotencia: %d",(pcarro+i)->potencia);
        printf("\nValor: %2.f",(pcarro+i)->valor);
        printf("\n--------------------------------------------");
    }
}

void desaloca(TipoCarro **pcarro)
{
    if(*pcarro==NULL)
    {
        printf("\nNao houve alocacao de memoria!");
        return;
    }
    free(*pcarro);
    *pcarro=NULL;
}
