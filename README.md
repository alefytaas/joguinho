#include<GL/glut.h>
#include<stdio.h>
#include<stdlib.h>

#define menuPrincipal 0
#define jogando 1
#define creditos 2
#define classificacao 3
#define sair 4
#define perdeu 5
#define DigNome 6
int flagColi=0;
int flagPosBarra=0;
int temp;
int temp1;
int flagVIDA = 3;
int flagBloco = 0;
static int tela[128][128];


static int keyUP=0, keyDOWN=0, keyLEFT=0, keyRIGHT=0, keyFIRE=0; //teclas w a d s fire é space

void keyPressed(unsigned char key, int x, int y){
	switch(key){
		case 'w':
			keyUP = 1;
			break;
		case 's':
			keyDOWN = 1;
			break;
		case 'a':
			keyLEFT = 1;
			break;
		case 'd':
			keyRIGHT = 1;
			break;
		case ' ':
			keyFIRE = 1;
			break;
	}
}

void keyReleased(unsigned char key, int x, int y){
	switch(key){
		case 'w':
			keyUP = 0;
			break;
		case 's':
			keyDOWN = 0;
			break;
		case 'a':
			keyLEFT = 0;
			break;
		case 'd':
			keyRIGHT = 0;
			break;
		case ' ':
			keyFIRE = 0;
			break;
	}
}

void keySpecialPressed(int key, int x, int y){
	switch(key){
		case GLUT_KEY_UP:
			keyUP = 1;
			break;
		case GLUT_KEY_DOWN:
			keyDOWN = 1;
			break;
		case GLUT_KEY_LEFT:
			keyLEFT = 1;
			break;
		case GLUT_KEY_RIGHT:
			keyRIGHT = 1;
			break;
	}
}

void keySpecialReleased(int key, int x, int y){

	//printf("%d \n",key); Capta botões de controle externos e mostra o código

	switch(key){
		case GLUT_KEY_UP:
			keyUP = 0;
			break;
		case GLUT_KEY_DOWN:
			keyDOWN = 0;
			break;
		case GLUT_KEY_LEFT:
			keyLEFT = 0;
			break;
		case GLUT_KEY_RIGHT:
			keyRIGHT = 0;
			break;
	}
}

//Codigo referente as fontes



int  u, v, z;
int x=0,y=0;
int Alfabeto[38][5][5]={
{//Letra A
{0,1,1,1,0},
{1,1,0,1,1},
{1,0,0,0,1},
{1,1,1,1,1},
{1,0,0,0,1}
},{//Letra B
{1,1,1,1,0},
{1,0,0,1,0},
{1,1,1,1,0},
{1,0,0,0,1},
{1,1,1,1,1}
},{//Letra C
{0,1,1,1,1},
{1,0,0,0,0},
{1,0,0,0,0},
{1,0,0,0,0},
{0,1,1,1,1}
},{//Letra D
{1,1,1,1,0},
{1,0,0,0,1},
{1,0,0,0,1},
{1,0,0,0,1},
{1,1,1,1,0}
},{//Letra E
{1,1,1,1,1},
{1,0,0,0,0},
{1,1,1,1,1},
{1,0,0,0,0},
{1,1,1,1,1}
},{//Letra F
{1,1,1,1,1},
{1,0,0,0,0},
{1,1,1,1,0},
{1,0,0,0,0},
{1,0,0,0,0}
},{//Letra G
{0,1,1,1,1},
{1,0,0,0,0},
{1,0,1,1,1},
{1,0,0,0,1},
{1,1,1,1,0}
},{//Letra H
{1,0,0,0,1},
{1,0,0,0,1},
{1,1,1,1,1},
{1,0,0,0,1},
{1,0,0,0,1}
},{//Letra I
{0,1,1,1,0},
{0,0,1,0,0},
{0,0,1,0,0},
{0,0,1,0,0},
{0,1,1,1,0}
},{//Letra J
{0,1,1,1,1},
{0,0,0,1,0},
{0,0,0,1,0},
{0,1,0,1,0},
{0,1,1,1,0}
},{//Letra K
{1,0,0,1,1},
{1,0,1,1,0},
{1,1,0,0,0},
{1,0,1,1,0},
{1,0,0,1,1}
},{//Letra L
{1,0,0,0,0},
{1,0,0,0,0},
{1,0,0,0,0},
{1,0,0,0,0},
{1,1,1,1,1}
},{//Letra M
{1,0,0,0,1},
{1,1,0,1,1},
{1,0,1,0,1},
{1,0,0,0,1},
{1,0,0,0,1}
},{//Letra N
{1,0,0,0,1},
{1,1,0,0,1},
{1,0,1,0,1},
{1,0,0,1,1},
{1,0,0,0,1}
},{//Letra O
{0,1,1,1,0},
{1,0,0,0,1},
{1,0,0,0,1},
{1,0,0,0,1},
{0,1,1,1,0}
},{//Letra P
{1,1,1,1,0},
{1,0,0,0,1},
{1,1,1,1,1},
{1,0,0,0,0},
{1,0,0,0,0}
},{//Letra Q
{0,1,1,1,0},
{1,0,0,0,1},
{1,0,0,0,1},
{1,0,1,1,0},
{0,1,1,1,1}
},{//Letra R
{1,1,1,1,0},
{1,0,0,0,1},
{1,1,1,1,0},
{1,0,0,1,0},
{1,0,0,0,1}
},{//Letra S
{0,1,1,1,1},
{1,0,0,0,0},
{0,1,1,1,0},
{0,0,0,0,1},
{1,1,1,1,0}
},{//Letra T
{1,1,1,1,1},
{0,0,1,0,0},
{0,0,1,0,0},
{0,0,1,0,0},
{0,0,1,0,0}
},{//Letra U
{1,0,0,0,1},
{1,0,0,0,1},
{1,0,0,0,1},
{1,0,0,0,1},
{0,1,1,1,0}
},{//Letra V
{1,0,0,0,1},
{1,1,0,1,1},
{0,1,0,1,0},
{0,0,1,0,0},
{0,0,1,0,0}
},{//Letra W
{1,0,1,0,1},
{1,0,1,0,1},
{1,0,1,0,1},
{0,1,1,1,1},
{0,1,1,1,0}
},{//Letra X
{1,0,0,0,1},
{0,1,0,1,0},
{0,0,1,0,0},
{0,1,0,1,0},
{1,0,0,0,1}
},{//Letra Y
{1,0,0,0,1},
{0,1,0,1,0},
{0,0,1,0,0},
{0,0,1,0,0},
{0,0,1,0,0}
},{//Letra Z
{1,1,1,1,1},
{0,0,0,1,0},
{0,0,1,0,0},
{0,1,0,0,0},
{1,1,1,1,1}
},{//Espaço em branco
{0,0,0,0,0},
{0,0,0,0,0},
{0,0,0,0,0},
{0,0,0,0,0},
{0,0,0,0,0}
},{//Número 0
{0,1,1,1,0},
{1,0,0,1,1},
{1,0,1,0,1},
{1,1,0,0,1},
{0,1,1,1,0}
},{//Número 1
{0,0,1,0,0},
{0,1,1,0,0},
{0,0,1,0,0},
{0,0,1,0,0},
{0,1,1,1,0}
},{//Número 2
{0,1,1,1,1},
{0,0,0,0,1},
{0,1,1,1,1},
{0,1,0,0,0},
{0,1,1,1,1}
},{//Número 3
{0,1,1,1,1},
{0,0,0,0,1},
{0,0,1,1,1},
{0,0,0,0,1},
{0,1,1,1,1}
},{//Número 4
{0,1,0,0,1},
{0,1,0,0,1},
{0,1,1,1,1},
{0,0,0,0,1},
{0,0,0,0,1}
},{//Número 5
{1,1,1,1,1},
{1,0,0,0,0},
{1,1,1,1,1},
{0,0,0,0,1},
{1,1,1,1,1}
},{//Número 6
{1,1,1,1,1},
{1,0,0,0,0},
{1,1,1,1,1},
{1,0,0,0,1},
{1,1,1,1,1}
},{//Número 7
{1,1,1,1,1},
{0,0,0,1,0},
{0,0,1,0,0},
{0,1,0,0,0},
{1,0,0,0,0}
},{//Número 8
{1,1,1,1,1},
{1,0,0,0,1},
{1,1,1,1,1},
{1,0,0,0,1},
{1,1,1,1,1}
},{//Número 9
{1,1,1,1,1},
{1,0,0,0,1},
{1,1,1,1,1},
{0,0,0,0,1},
{1,1,1,1,1}
},{// -
{0,0,0,0,0},
{0,0,0,0,0},
{1,1,1,1,1},
{0,0,0,0,0},
{0,0,0,0,0}
}};



char nome[21];
char name0[21];
char name[21];
char nome2[21];
char name1[21];
char name2[21];
char name3[21];
char name4[21];
char name5[21];
char nome1[21];
char quest[21];
char nao[21];
char sim[21];
char vida[21];
char jogador[10];
int caractere;
int pos = 0;
char n1[21];
char term[21];
char ran[21];
char fim[21];



// o codigo referente a bola começa aqui

int bola[4][4]={
{0,0,0,0},
{0,1,1,0},
{0,1,1,0},
{0,0,0,0}
};

int posBolaX = 60, posBolaY = 116; //posição inicial da bola
int flagFire = 0; //flag

//float float_posBolaX = 50, float_posBolaY=120;
//float movX=0.7071,movY=.7071;


int movX=-1, movY=-1;

int blocos[10][10] = {
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
	{1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
};

int posBarraX = 60, posBarraY = 120, largBarra = 60;

//int playing = jogando;
int playing;
playing= menuPrincipal;

int flagKeyFIRE = 0;
int flagKeyFIRE1 = 0;

void atualizaTela(){


//USO O COMPILADOR DA LINHA DE COMANDO LINUX
//COMANDO:

//gcc -o joguinho joguinho.c -lGL -lGLU -lglut &&./joguinho


// Apaga Tela


int i,j;

for(i=0;i<128;i++)
	for(j=0;j<128;j++)
	tela[i][j]=0;



switch (playing) {
	case jogando:
	//Desenha Bola
	// finalização
if(flagBloco == 10){
flagBloco = 0;
sprintf(fim, "%s", "Game End");
	for(i=0; i<6; i++){
		if(fim[i] >= 'a' && fim[i] <= 'z')
			caractere = fim[i] - 'a';
		else
			if(fim[i] >= 'A' && fim[i] <='Z')
				caractere = fim[i] - 'A';
			else
				if(fim[i] == ' ')
					caractere = 26;
				else
					if(fim[i] >= '0' && fim[i] <= '9')
						caractere = 27 + fim[i] - '0';

		for(x=0;x<5;x++){
			for(y=0;y<5;y++)
			tela[y + i*6 + 17][x+60]=Alfabeto[caractere][x][y];
		}
	}


}


	for(i=0;i<4;i++){
		for(j=0;j<4;j++){
			tela[i+posBolaX][j+posBolaY]=bola[j][i];
		}
	}


	int u, v, o;
	//for paredes.

	for (u=0; u<128; u++){
	tela[1][u]=1; //esquerda
	tela[u][5]=1; //cima
	tela[126][u]=1; //direita
	tela[u][126]=1; //baixo
	}

	// For barraflagVIDA

	for (o = 0; o<largBarra; o++){ //tamanho barra
		tela[posBarraX+o][120]=1;
	}
			if(keyRIGHT  && posBarraX < 126 - largBarra){
				posBarraX = posBarraX+1;}
			if(keyLEFT && posBarraX > 2){
				posBarraX = posBarraX-1;}

			if(posBolaX + 4 >= posBarraX && posBolaX <= posBarraX + largBarra && posBolaY == posBarraY - 3)

					movY=movY*-1;

			//if (posBarraX>121 && posBarraX < 3)
				//movY=movY*-1;

	//for blocos

	int larBloco=10,altBloco=4;

	int posBlocoAtualX, posBlocoAtualY;

	int flagX = 1;
	int flagY = 1;

	int k,l;

	for (i=0;i<10;i++)
		for (j=0;j<10;j++){
			if (blocos[i][j]==1){ //espaçamento entre os blocos

				posBlocoAtualX = 5 + i*(larBloco+2);
				posBlocoAtualY = 16 + j*(altBloco+2);

				if ( //controle de colisão
					posBolaX + 4 >= posBlocoAtualX &&
					posBolaX <= posBlocoAtualX + larBloco &&
					posBolaY + 4 >= posBlocoAtualY &&
					posBolaY <= posBlocoAtualY + altBloco
				){
					blocos[i][j] = 0; //pós colisão "flag 0"
//Colisão

					if(flagX && (posBolaX + 4 == posBlocoAtualX || posBolaX == posBlocoAtualX + larBloco)){
						movX=movX*-1;
						flagX=0;
						flagColi++;
						flagBloco++;
					}
					if(flagY && (posBolaY + 4 == posBlocoAtualY || posBolaY == posBlocoAtualY + altBloco)){
						movY=movY*-1;
						flagY = 0;
						flagColi++;
						flagBloco++;
					}
				}else
					for (k=0;k<larBloco;k++)
						for (l=0;l<altBloco;l++)
							tela[posBlocoAtualX+k][posBlocoAtualY+l]=1;
			}
		}

	//Muda ângulo da bola, com 30° - B

	if(posBolaX>121 || posBolaX < 3)
		movX=movX*-1;

	if (/*posBolaY>121 || */posBolaY < 3) //lance do chao
		movY=movY*-1;

	if (posBolaY>121){
		flagColi=flagColi-10;
		printf("Tu perdeu preiboy\n");
		flagFire = 0;
		posBolaX = 60;
		posBolaY = 116;
		movX = -1;
		playing = perdeu;
		flagVIDA = flagVIDA - 1;
		//movY = 1;
	}

	if (keyFIRE)
	flagFire = 1;
	if (flagFire){
		posBolaX=posBolaX+movX;
		posBolaY=posBolaY+movY;
	}else{
		posBolaX = posBarraX + largBarra/2 - 2; //bola volta a posição inicial
	}

	//float_posBolaX=float_posBolaX+movX;
	//float_posBolaY=float_posBolaY+movY;


	sprintf(nome, "%20d", flagColi);
				for(i=0; i<20; i++){
					if(nome[i] >= 'a' && nome[i] <= 'z')
						caractere = nome[i] - 'a';
					else
						if(nome[i] >= 'A' && nome[i] <='Z')
							caractere = nome[i] - 'A';
						else
							if(nome[i] == ' ')
								caractere = 26;
							else
								if(nome[i] >= '0' && nome[i] <= '9')
									caractere = 27 + nome[i] - '0';

					for(x=0;x<5;x++){
						for(y=0;y<5;y++)
						tela[y + i*6 + 4][x]=Alfabeto[caractere][x][y];
					}
				}


		for(i=0; i<10; i++){
					caractere = jogador[i];
						for(x=0;x<5;x++){
							for(y=0;y<5;y++)
								tela[y + i*6 + 4][x]=Alfabeto[caractere][x][y];
						}

	}
		break;

		case perdeu:// fazer
if(flagVIDA ==  0){
flagColi = 0;
flagVIDA = 3;
for (i=0;i<10;i++)
	for (j=0;j<10;j++){
		blocos[i][j] =1;
}}

		sprintf(quest, "%s", "Deseja continuar");
			for(i=0; i<16; i++){
				if(quest[i] >= 'a' && quest[i] <= 'z')
					caractere = quest[i] - 'a';
				else
					if(quest[i] >= 'A' && quest[i] <='Z')
						caractere = quest[i] - 'A';
					else
						if(quest[i] == ' ')
							caractere = 26;
						else
							if(quest[i] >= '0' && quest[i] <= '9')
								caractere = 27 + quest[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 17][x+60]=Alfabeto[caractere][x][y];
				}
			}
		sprintf(sim, "%s", "sim");
			for(i=0; i<3; i++){
				if(sim[i] >= 'a' && sim[i] <= 'z')
					caractere = sim[i] - 'a';
				else
					if(sim[i] >= 'A' && sim[i] <='Z')
						caractere = sim[i] - 'A';
					else
						if(sim[i] == ' ')
							caractere = 26;
						else
							if(sim[i] >= '0' && sim[i] <= '9')
								caractere = 27 + sim[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 10][x+70]=Alfabeto[caractere][x][y];
}}
		sprintf(nao, "%s", "nao");
			for(i=0; i<3; i++){
				if(nao[i] >= 'a' && nao[i] <= 'z')
					caractere = nao[i] - 'a';
				else
					if(nao[i] >= 'A' && nao[i] <='Z')
						caractere = nao[i] - 'A';
					else
						if(nao[i] == ' ')
							caractere = 26;
						else
							if(nao[i] >= '0' && nao[i] <= '9')
								caractere = 27 + nao[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 105][x+70]=Alfabeto[caractere][x][y];
}}
		sprintf(vida, "%s %3d", "VIDA", flagVIDA);
			for(i=0; i<8; i++){
				if(vida[i] >= 'a' && vida[i] <= 'z')
					caractere = vida[i] - 'a';
				else
					if(vida[i] >= 'A' && vida[i] <='Z')
						caractere = vida[i] - 'A';
					else
						if(vida[i] == ' ')
							caractere = 26;
						else
							if(vida[i] >= '0' && vida[i] <= '9')
								caractere = 27 + vida[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 6][x+6]=Alfabeto[caractere][x][y];
}}


					if (keyLEFT) {
					playing = jogando;
				}	if (keyRIGHT){
					playing = menuPrincipal;
					flagColi = 0;
					flagBloco = 0;
					for (i=0;i<10;i++) // reinicia blocos
						for (j=0;j<10;j++){
							blocos[i][j] =1;
}

}
		break;
case DigNome: {


					if (keyLEFT) {
					playing = menuPrincipal;
				}

		sprintf(term, "%s", "Terminou");
			for(i=0; i<8; i++){
				if(term[i] >= 'a' && term[i] <= 'z')
					caractere = term[i] - 'a';
				else
					if(term[i] >= 'A' && term[i] <='Z')
						caractere = term[i] - 'A';
					else
						if(term[i] == ' ')
							caractere = 26;
						else
							if(term[i] >= '0' && term[i] <= '9')
								caractere = 27 + term[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 15][x+62]=Alfabeto[caractere][x][y];
}}

		sprintf(sim, "%s", "sim");
			for(i=0; i<3; i++){
				if(sim[i] >= 'a' && sim[i] <= 'z')
					caractere = sim[i] - 'a';
				else
					if(sim[i] >= 'A' && sim[i] <='Z')
						caractere = sim[i] - 'A';
					else
						if(sim[i] == ' ')
							caractere = 26;
						else
							if(sim[i] >= '0' && sim[i] <= '9')
								caractere = 27 + sim[i] - '0';

				for(x=0;x<5;x++){
					for(y=0;y<5;y++)
					tela[y + i*6 + 10][x+70]=Alfabeto[caractere][x][y];
}}



jogador[10] = 26,26,26,26,26,26,26,26,26,26;

	if(keyUP && !temp){
		temp=10;
		jogador[pos]++;}
		if(jogador[pos] > 37)
			jogador[pos]=0;
	if(keyDOWN && !temp){
		temp=10;
		jogador[pos]--;}
		if(jogador[pos] < 0)
			jogador[pos]=37;
	if(keyFIRE && !temp){
		temp=10;
		pos++;}
		if(pos>9)
			pos=0;
if (temp > 0)
temp--;

		//sprintf(jogador[10], "%s");
			for(i=0; i<10; i++){
				caractere = jogador[i];
					for(x=0;x<5;x++){
						for(y=0;y<5;y++)
							tela[y + i*6 + 44][x+114]=Alfabeto[caractere][x][y];
					}

}
}
break;

		case menuPrincipal: {

		sprintf(name, "%s %d", "Jogar", flagColi);

			for(i=0; i<6; i++){
				if(name[i] >= 'a' && name[i] <= 'z')
					caractere = name[i] - 'a';
				else
					if(name[i] >= 'A' && name[i] <='Z')
						caractere = name[i] - 'A';
					else
						if(name[i] == ' ')
							caractere = 26;
						else
							if(name[i] >= '0' && name[i] <= '9')
								caractere = 27 + name[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 44][x+114]=Alfabeto[caractere][x][y];
					}

}
								//if (keyFIRE )
								//playing = jogando;

	sprintf(name1, "%s %d", "Credito", flagColi);

			for(i=0; i<7; i++){
				if(name1[i] >= 'a' && name1[i] <= 'z')
					caractere = name1[i] - 'a';
				else
					if(name1[i] >= 'A' && name1[i] <='Z')
						caractere = name1[i] - 'A';
					else
						if(name1[i] == ' ')
							caractere = 26;
						else
							if(name1[i] >= '0' && name1[i] <= '9')
								caractere = 27 + name1[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 86][x+114]=Alfabeto[caractere][x][y];
					}

}
sprintf(n1, "%s %d", "Digite o seu nome", flagColi);

			for(i=0; i<17; i++){
				if(n1[i] >= 'a' && n1[i] <= 'z')
					caractere = n1[i] - 'a';
				else
					if(n1[i] >= 'A' && n1[i] <='Z')
						caractere = n1[i] - 'A';
					else
						if(n1[i] == ' ')
							caractere = 26;
						else
							if(n1[i] >= '0' && n1[i] <= '9')
								caractere = 27 + n1[i] - '0';


									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 8][x+102]=Alfabeto[caractere][x][y];
					}

}

sprintf(n1, "%s %d", "BREAKER", flagColi);

			for(i=0; i<7; i++){
				if(n1[i] >= 'a' && n1[i] <= 'z')
					caractere = n1[i] - 'a';
				else
					if(n1[i] >= 'A' && n1[i] <='Z')
						caractere = n1[i] - 'A';
					else
						if(n1[i] == ' ')
							caractere = 26;
						else
							if(n1[i] >= '0' && n1[i] <= '9')
								caractere = 27 + n1[i] - '0';


									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 45][x+35]=Alfabeto[caractere][x][y];
					}

}

sprintf(nome1, "%s %d", "Rank", flagColi);

			for(i=0; i<4; i++){
				if(nome1[i] >= 'a' && nome1[i] <= 'z')
					caractere = nome1[i] - 'a';
				else
					if(nome1[i] >= 'A' && nome1[i] <='Z')
						caractere = nome1[i] - 'A';
					else
						if(nome1[i] == ' ')
							caractere = 26;
						else
							if(nome1[i] >= '0' && nome1[i] <= '9')
								caractere = 27 + nome1[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 8][x+114]=Alfabeto[caractere][x][y];
					}

}
/*sprintf(nome1, "%s %d", "DigNome", flagColi);

			for(i=0; i<4; i++){
				if(nome2[i] >= 'a' && nome2[i] <= 'z')
					caractere = nome2[i] - 'a';
				else
					if(nome2[i] >= 'A' && nome2[i] <='Z')
						caractere = nome2[i] - 'A';
					else
						if(nome2[i] == ' ')
							caractere = 26;
						else
							if(nome2[i] >= '0' && nome2[i] <= '9')
								caractere = 27 + nome2[i] - '0';


									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 8][x+20]=Alfabeto[caractere][x][y];
					}

}

*/



for (o = 0; o<largBarra; o++){ // barra seleção menu
		tela[posBarraX+o][posBarraY]=1;
	}
			if(keyRIGHT && !temp){
				temp=10;
			if(flagPosBarra<1)
				flagPosBarra = flagPosBarra+1;}
			if(keyLEFT && !temp){
				temp=10;
			if(flagPosBarra>-2)
				flagPosBarra = flagPosBarra-1;}

}
if (temp > 0)
temp--;

//Alteração Jonathan bug manu

switch (flagPosBarra){
case 0:
	posBarraY = 120;
	posBarraX = 50;
	if(posBarraX == 50 && keyFIRE)
		//playing = jogando;
		flagKeyFIRE = 1;
	if(flagKeyFIRE && !keyFIRE){
		flagKeyFIRE = 0;
		playing = jogando;
	}
	break;

case -1:
	posBarraY = 120;
	posBarraX = 10;
	if(posBarraX == 10 && keyFIRE)
		//playing = classificacao;
		flagKeyFIRE = 1;
	if(flagKeyFIRE && !keyFIRE){
		flagKeyFIRE = 0;
		playing = classificacao;
	}
	break;

case 1:
	posBarraY = 120;
	posBarraX = 100;
	if(posBarraX == 100 && keyFIRE)
		//playing = creditos;
		flagKeyFIRE = 1;
	if(flagKeyFIRE && !keyFIRE){
		flagKeyFIRE = 0;
		playing = creditos;
	}
	break;
case -2:
	posBarraY = 108;
	posBarraX = 10;
	if(posBarraX == 10 && posBarraY == 108 && keyFIRE)
		//playing = creditos;
		flagKeyFIRE = 1;
	if(flagKeyFIRE && !keyFIRE){
		flagKeyFIRE = 0;
		playing = DigNome;
	}
	break;
}

break;

	case creditos:{
sprintf(name2, "%s %d", "Ed Carlos Pessoa", flagColi);

			for(i=0; i<16; i++){
				if(name2[i] >= 'a' && name2[i] <= 'z')
					caractere = name2[i] - 'a';
				else
					if(name2[i] >= 'A' && name2[i] <='Z')
						caractere = name2[i] - 'A';
					else
						if(name2[i] == ' ')
							caractere = 26;
						else
							if(name2[i] >= '0' && name2[i] <= '9')
								caractere = 27 + name2[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 10][x+10+20]=Alfabeto[caractere][x][y];
					}

}


sprintf(name3, "%s %d", "Fernando Carlos", flagColi);

			for(i=0; i<15; i++){
				if(name3[i] >= 'a' && name3[i] <= 'z')
					caractere = name3[i] - 'a';
				else
					if(name3[i] >= 'A' && name3[i] <='Z')
						caractere = name3[i] - 'A';
					else
						if(name3[i] == ' ')
							caractere = 26;
						else
							if(name3[i] >= '0' && name3[i] <= '9')
								caractere = 27 + name3[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 10][x+18+20]=Alfabeto[caractere][x][y];
					}

}
sprintf(name4, "%s %d", "Thalia Gurgel", flagColi);

			for(i=0; i<13; i++){
				if(name4[i] >= 'a' && name4[i] <= 'z')
					caractere = name4[i] - 'a';
				else
					if(name4[i] >= 'A' && name4[i] <='Z')
						caractere = name4[i] - 'A';
					else
						if(name4[i] == ' ')
							caractere = 26;
						else
							if(name4[i] >= '0' && name4[i] <= '9')
								caractere = 27 + name4[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 10][x+26+20]=Alfabeto[caractere][x][y];
					}

}
sprintf(name5, "%s %d", "Thiago Alefy", flagColi);

			for(i=0; i<13; i++){
				if(name5[i] >= 'a' && name5[i] <= 'z')
					caractere = name5[i] - 'a';
				else
					if(name5[i] >= 'A' && name5[i] <='Z')
						caractere = name5[i] - 'A';
					else
						if(name5[i] == ' ')
							caractere = 26;
						else
							if(name5[i] >= '0' && name5[i] <= '9')
								caractere = 27 + name5[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 10][x+34+20]=Alfabeto[caractere][x][y];
					}

}
sprintf(name0, "%s %d", "Programadores", flagColi);

			for(i=0; i<13; i++){
				if(name0[i] >= 'a' && name0[i] <= 'z')
					caractere = name0[i] - 'a';
				else
					if(name0[i] >= 'A' && name0[i] <='Z')
						caractere = name0[i] - 'A';
					else
						if(name0[i] == ' ')
							caractere = 26;
						else
							if(name0[i] >= '0' && name0[i] <= '9')
								caractere = 27 + name0[i] - '0';

									for(x=0;x<5;x++){
										for(y=0;y<5;y++)
											tela[y + i*6 + 20][x+6]=Alfabeto[caractere][x][y];
					}

}

if (flagKeyFIRE1 == 0 && keyFIRE == 1) {
	flagKeyFIRE1 = 1;
}

if(flagKeyFIRE1 == 1 && keyFIRE ==0){ // comando Jonathan
 flagKeyFIRE1 = 0;
 playing = menuPrincipal;
}


}

break;


case (classificacao):{

	sprintf(ran, "%s", "Ranking");

				for(i=0; i<7; i++){
					if(ran[i] >= 'a' && ran[i] <= 'z')
						caractere = ran[i] - 'a';
					else
						if(ran[i] >= 'A' && ran[i] <='Z')
							caractere = ran[i] - 'A';
						else
							if(ran[i] == ' ')
								caractere = 26;
							else
								if(ran[i] >= '0' && ran[i] <= '9')
									caractere = 27 + ran[i] - '0';

										for(x=0;x<5;x++){
											for(y=0;y<5;y++)
												tela[y + i*6 + 45][x+15]=Alfabeto[caractere][x][y];
						}

	}

if (flagKeyFIRE1 == 0 && keyFIRE == 1) {
	flagKeyFIRE1 = 1;
}

if(flagKeyFIRE1 == 1 && keyFIRE ==0){ // comando Jonathan
 flagKeyFIRE1 = 0;
 playing = menuPrincipal;
}
			}
		}

	}
//}

void desenha(){
	int i, j;

	for(i=0; i<128; i++){
		for(j=0; j<128; j++){
			if(tela[i][j])
				glColor3f(1, 1, 1);
			else
				glColor3f(0, 0, 0);

			glBegin(GL_QUADS);
				glVertex2f(i,j+1);
				glVertex2f(i,j);
				glVertex2f(i+1,j);
				glVertex2f(i+1,j+1);
			glEnd();
		}
	}

	atualizaTela();

	glutSwapBuffers();

	usleep(5000);

	glutPostRedisplay();
}

int main(int argc, char ** argv){
	glutInit(&argc, argv);

	glMatrixMode(GL_MODELVIEW);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);

	glutInitWindowSize(640, 640);
	glutCreateWindow("Joguinho");

	gluOrtho2D(0.0, 128.0, 128.0, 0.0);

	glutDisplayFunc(desenha);

	glutKeyboardFunc(keyPressed);
	glutKeyboardUpFunc(keyReleased);

	glutSpecialFunc(keySpecialPressed);
	glutSpecialUpFunc(keySpecialReleased);

	glutMainLoop();

	return 0;
}
