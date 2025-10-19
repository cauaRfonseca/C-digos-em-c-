#include <iostream>
#include <ctime>
#include <cstdlib>
#include <conio.h>
using namespace std;

struct Status{
	int vida, dano;
	string nome, ataques[2], raridade;

};

int main() {
	Status equipe[6];
	
	int a, e, i, j, coordM[2], coordC[2], chance = 1, fugar, lista, party = 1, opcao, cont, vidaM, vidaT[6], captura, ataque, ataqueM, derrotados, pokebolas, inicial, acc;
	char player, movimento;
	bool inCasa = false, fuga, capturado = false, master = true, bauM = false;
	string nickname;
	
	coordM[0] = 6;
	coordM[1] = 4;
	
	Status pokemon[13] = {
		{35, 10, "Caterpie", {"Bug Bite", "Flock"}, "Comum"},
		{30, 12, "Weedle", {"Bug Bite", "Tackle"}, "Comum"},
		{45, 15, "Fletchlin", {"Extreme Speed", "Ember"}, "Comum"},
		{40, 15, "Pancham", {"Tackle", "Parting Shot"}, "Comum"},
		{40, 15, "Mareep", {"Eletric Wave", "Tackle"}, "Comum"},
		{60, 20, "Pikachu", {"Thunder Bolt", "Eletric ball"}, "Incomum"},
		{65, 20, "Ursaring", {"Rock Smash", "Punch"}, "Incomum"},
		{50, 15, "Sandile", {"Dig", "Tackle"}, "Incomum"},
		{50, 10, "Riolu", {"Quick Attack", "Close Combat"}, "Incomum"},
		{95, 30, "Beldum", {"Psychic", "Rock Polish"}, "Raro"},
		{85, 30, "Heracross", {"Horn Atttack", "Cut"}, "Raro"},
		{80, 35, "Hawlucha", {"Low Kick", "Poison Jab"}, "Raro"},
		{999, 29, "Bidoof", {"Judgement", "Punish"}, "Lendario"},
	};
	
	equipe[1].vida = 0;
	equipe[2].vida = 0;
	equipe[3].vida = 0;
	equipe[4].vida = 0;
	equipe[5].vida = 0;
	
	cout << "\n\tInsira o seu nickname: ";
	cin >> nickname;
	cout << "\n\tInsira o caracter desejado: ";
	cin >> player;
	system("cls");
	
	for(i = 0; i < 6; i++){
		equipe[i].nome = ".";
	}
	
	const char mapa[20][30] = {
		{'~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '#', '#', '#', '#', '#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '#', '-', '-', '-', '#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '#', '-', '-', '-', '#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '#', '#', 'P', '#', '#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', '_', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', 'w', '~'},
		{'~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~', '~'},
	};
	
	const char casa[8][11] = {
		{'#', '#', '#', '#', '#', '#', '#', '#', '#', '#', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', '_', '#'},
		{'#', '_', '_', '_', '_', '_', '_', '_', '_', 'M', '#'},
		{'#', '#', '#', '#', '#', 'E', '#', '#', '#', '#', '#'},
	};
	
	system("cls");
	cout << "\n\tSeja bem-vindo ao mundo Pokemon C++, " << nickname << "!\n\tEscolha seu Pokemon inicial para comecar sua jornada:\n\t1 - Treecko\n\t2 - Swobble\n\t3 - Fuecoco\n\t---> ";
	do{
		cin >> inicial;
		switch(inicial){
			case 1: 
				equipe[0] = {60, 20, "Treecko", {"Grass knot", "Bullet seed"}, "Inicial"};
				break;
			case 2:
				equipe[0] = {55, 20, "Swobble", {"Bubble", "Water beam"}, "Inicial"};
				break;
			case 3:
				equipe[0] = {60, 20, "Fuecoco", {"Flamethrower", "Ember"}, "Inicial"};
				break;
			default: cout << "\n\tInicial invalido! Tente novamente: ";
		}
	}while((inicial<1)||(inicial>3));
	system("cls");
	
	do{
		fuga = false;
		
   	cout << "\n\t" << nickname << " | Equipe atual: " << party << " [E]";
    	cout << "\n\t";
    	
    	if (inCasa){
    		for (i = 0; i < 8; i++){
			   for (j = 0; j < 11; j++){
		 		   if ((i==coordC[0])&&(j==coordC[1])){
		         	cout << player << " ";
		      	}else{
	   				cout << casa[i][j] << " ";
		        }
		      }
		   	cout << "\n\t";
		   }
		}else{
	    	for (i = 0; i < 20; i++){
			   for (j = 0; j < 30; j++){
		 		   if ((i==coordM[0])&&(j==coordM[1])){
		         	cout << player << " ";
		         	if (mapa[i][j]=='w'){
		         		unsigned seed = time(0);
	          			srand (seed);
	          			chance = 1+rand() % 50;
		          		lista = 1+rand() % 10;
		         	}
		      	}else{
	   				cout << mapa[i][j] << " ";
		        }
		      }
		   	cout << "\n\t";
		   }
	   }
	   if (chance>=40){
	   	fuga = false;
	   	capturado = false;
	   	cont = 0;
	   	derrotados = 0;
	   	e = 0;
	   	pokebolas = 15;
	   	cout << "\n\tVoce encontrou um Pokemon!\n\t";
	   	a = lista;
	   	system("pause");
			;
	   	system("cls");
	   	vidaM = pokemon[a-1].vida;
	   	for (i = 0; i < 6; i++){
	   		vidaT[i] = equipe[i].vida;
			}
	   	do{
	   		if (cont==0){
					cout << "\n\tVoce encontrou um " << pokemon[a-1].nome << " selvagem!\n";
				}
		   	cout << "\n\t| " << pokemon[a-1].nome << " | HP: " << vidaM;
		  		if (party>0){
					cout << "\n\n\t\t| " << equipe[e].nome << " | HP: " << vidaT[e];
				}
				cout << "\n\n\tPokebolas: " << pokebolas << "\n\t" << nickname << ", o que voce deseja fazer?\n\t1 - Lutar\t2 - Capturar\n\t3 - Equipe\t4 - Fugir\n\n\t---> ";
		    	cin >> opcao;
		    	switch (opcao){
		    		case 1:
						system("cls");
						ataqueM = 1+rand() % 2;
						cout << "\n\n\t| " << equipe[e].nome << " | HP: " << vidaT[e];
						cout << "\n\n\tQual ataque " << equipe[e].nome << " deve usar?\n\t1 - " << equipe[e].ataques[0] << "\t2 - " << equipe[e].ataques[1] << "\n\n\t---> ";
    					cin >> ataque;
    					system("cls");
    					cout << "\n\t" << equipe[e].nome << " usou " << equipe[e].ataques[ataque-1];
    					vidaM -= equipe[e].dano;
    					if (vidaM>0){
    						ataqueM = 1+rand() % 2;
    						if (ataqueM==1){
    							cout << "\n\t" << pokemon[a-1].nome << " usou " << pokemon[a-1].ataques[0] << "!\n";
							}else{
								cout << "\n\t" << pokemon[a-1].nome << " usou " << pokemon[a-1].ataques[1] << "!\n";
							}vidaT[e] -= pokemon[a-1].dano;
							if (vidaT[e]<=0){
								cout << "\n\t" << equipe[e].nome << " foi derrotado!\n\t";
								system("pause");
								system("cls");
								derrotados++;
								if ((derrotados==party)&&(derrotados>0)){
									cout << "\n\tToda sua equipe foi derrotada!\n\n";
									system ("pause");
								}else{
									cout << "\n\tEscolha um novo pokemon para usar!";
									for (i = 0; i < 6; i++){
										cout << "\n\t" << i+1 << " - " << equipe[i].nome;
										if ((vidaT[i]<=0)&&(equipe[i].nome!=".")){
										cout << " - DERROTADO";
										}
									}
									cout << "\n\tQual pokemon voce quer usar?\n\t---> ";
									do{
										cin >> e;
										if ((e<=0)||(e>=7)){
											e = 0;
											cout << "\n\tPokemon inexistente! Tente novamente: ";
										}else{
											if (equipe[e-1].nome=="."){
												cout << "\n\tPeokemon inexistente! Tente novamente: ";
											}else{
												if ((vidaT[e-1]<=0)&&(equipe[e-1].nome!=".")){
													cout << "\n\tEsse Pokemon esta derrotado! Tente outro: ";
												}
											}
										}
									}while((equipe[e-1].nome==".")||(e<=0)||(e>=7)||(vidaT[e-1]<=0));
									e--;
									system("cls");
								}
	    					}
						}else{
							system("cls");
							cout << "\n\t" << pokemon[a-1].nome << " foi derrotado!\n\t";
							system("pause");
							system("cls");
						}break;
					case 2:
						if (pokebolas>0){
							if (pokemon[a-1].raridade=="Comum"){
								captura = 1+rand() % 2;
							}else{
								if (pokemon[a-1].raridade=="Incomum"){
									captura = 1+rand() % 4;
								}else{
									if (pokemon[a-1].raridade=="Raro"){
										captura = 1+rand() % 7;
									}else{
										if (pokemon[a-1].raridade=="Lendario"){
											captura = 1+rand() % 20;
										}
									}
								}
							}
							if (captura==1){
								capturado = true;
							}else{
								capturado = false;
							}
							cout << "\n\tVoce arremessou uma Pokebola e . . .";
							if (capturado){
								cout << "\n\t" << pokemon[a-1].nome << " foi capturado!\n\t";
								equipe[party].nome = pokemon[a-1].nome;
								equipe[party].vida = pokemon[a-1].vida;
								equipe[party].ataques[0] = pokemon[a-1].ataques[0];
								equipe[party].ataques[1] = pokemon[a-1].ataques[1];
								equipe[party].dano = pokemon[a-1].dano;
								vidaM = 0;
								party++;
								system("pause");
								system ("cls");
							}else{
								cout << "\n\tA Pokebola quebrou!\n\t";
								system("pause");
								system("cls");
							}pokebolas--;
						}else{
							cout << "\n\tSuas Pokebolas acabaram!\n\t";
							system("pause");
							system("cls");
						}
						break;
					case 3:
						system("cls");
						cout << "\n\tEquipe atual:";
						for (i = 0; i < 6; i++){
							cout << "\n\t" << i+1 << " - " << equipe[i].nome;
							if ((vidaT[i]<=0)&&(equipe[i].nome!=".")){
								cout << " - DERROTADO";
							}
						}
						cout << "\n\tQual pokemon voce quer usar?\n\t---> ";
						do{
							cin >> e;
							if ((e<=0)||(e>=7)){
								e = 0;
								cout << "\n\tPokemon inexistente! Tente novamente: ";
							}else{
								if (equipe[e-1].nome=="."){
									cout << "\n\tPeokemon inexistente! Tente novamente: ";
								}else{
									if ((vidaT[e-1]<=0)&&(equipe[e-1].nome!=".")){
										cout << "\n\tEsse Pokemon esta derrotado! Tente outro: ";
									}
								}
							}
						}while((equipe[e-1].nome==".")||(e<=0)||(e>=7)||(vidaT[e-1]<=0));
						e--;
						system("cls");
						break;                                                      
					case 4:
						fugar = 1+rand() % 3;
						if (fugar==1){
							fuga = true;
							cout << "\n\tVoce fugiu!\n\t";
							system("pause");
						}else{
							cout << "\n\tVoce nao conseguiu fugir!\n\t";
							system("pause");
							cont++;
						}system("cls");
						break;
					case 11:
						if (master){
							cout << "\n\tVoce nao possui nenhuma Master Ball!\n\t";
							system("pause");
							system("cls");
						}else{
							master = true;
							cout << "\n\tVoce arremessou uma Masterball e . . .";
							cout << "\n\t" << pokemon[a-1].nome << " foi capturado!\n\t";
							equipe[party].nome = pokemon[a-1].nome;
							equipe[party].vida = pokemon[a-1].vida;
							equipe[party].ataques[0] = pokemon[a-1].ataques[0];
							equipe[party].ataques[1] = pokemon[a-1].ataques[1];
							equipe[party].dano = pokemon[a-1].dano;
							vidaM = 0;
							party++;
							system("pause");
							system ("cls");
							capturado = true;
						}
					default: system("cls");
				}cont++;
	    	}while(((derrotados!=party)||(derrotados==0))&&(fuga==false)&&(capturado==false)&&(vidaM>0));
	    	system("cls");
		}else{
			cout << "\n\tUse WASD para se mover! ";
	   	movimento = _getch();
	   	if (inCasa){
	   		//Dentro da casa
		   	switch (movimento){
		    		case 'w': case 'W': coordC[0] -= 1; break;
		      	case 'a': case 'A': coordC[1] -= 1; break;
		      	case 's': case 'S': coordC[0] += 1; break;
		      	case 'd': case 'D': coordC[1] += 1; break;
		      	case 'e': case 'E':
		      		system("cls");
		      		cout << "\n\t" << nickname << " | Equipe atual: " << party << " [E]";
		      		for (i = 0; i < 6; i++){
							cout << "\n\t" << i+1 << " - " << equipe[i].nome;
						}cout << "\n\n\t";
						system("pause");
						system("cls");
				}
		   	if ((casa[coordC[0]][coordC[1]]=='~')||(casa[coordC[0]][coordC[1]]=='#')|(casa[coordC[0]][coordC[1]]=='M')){
		   		if (casa[coordC[0]][coordC[1]]=='M'){
		   			if (bauM){
							cout << "\n\tVoce ja resgatou sua Master Ball!\n\t";
							system("pause");
						}else{
							master = false;
							bauM = true;
							cout << "\n\tVoce resgatou uma Master Ball!\n\t";
							system("pause");
						}
					}
					switch (movimento){
			    		case 'w': case 'W': coordC[0] += 1; break;
			      	case 'a': case 'A': coordC[1] += 1; break;
			      	case 's': case 'S': coordC[0] -= 1; break;
			      	case 'd': case 'D': coordC[1] -= 1; break;
			   	}
				}
				if (casa[coordC[0]][coordC[1]]=='E'){
					inCasa = false;
					coordM[0] = 6;
					coordM[1] = 4;
				}
			}else{
				//Fora da casa
				switch (movimento){
		    		case 'w': case 'W': coordM[0] -= 1; break;
		      	case 'a': case 'A': coordM[1] -= 1; break;
		      	case 's': case 'S': coordM[0] += 1; break;
		      	case 'd': case 'D': coordM[1] += 1; break;
		      	case 'e': case 'E':
		      		system("cls");
		      		cout << "\n\t" << nickname << " | Equipe atual: " << party << " [E]";
		      		for (i = 0; i < 6; i++){
							cout << "\n\t" << i+1 << " - " << equipe[i].nome;
						}cout << "\n\n\t";
						system("pause");
						system("cls");
				}
		   	if ((mapa[coordM[0]][coordM[1]]=='~')||(mapa[coordM[0]][coordM[1]]=='#')){
					switch (movimento){
			    		case 'w': case 'W': coordM[0] += 1; break;
			      	case 'a': case 'A': coordM[1] += 1; break;
			      	case 's': case 'S': coordM[0] -= 1; break;
			      	case 'd': case 'D': coordM[1] -= 1; break;
			   	}
				}
				if (mapa[coordM[0]][coordM[1]]=='P'){
					inCasa = true;
					coordC[0] = 6;
					coordC[1] = 5;
				}
			}system ("cls");
		}
 	}while(party<6);
 	system("cls");
 	cout << "\n\tCONQUISTA: | Mestre Pokemon |\n\tParabens, voce completou uma equipe pokemon, seu objetivo foi concluido\n\tAte mais! :)";
}
