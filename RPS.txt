#include <iostream>
#include <windows.h>
using namespace::std;

enum RPS{rock = 1 , paper = 2 , scissor = 3};
void Title() {
	cout << "-------------------------------------------------------" <<"\n" << endl;
	cout << "                    Welcome to RPS Game                " << "\n" << endl;
	cout << "-------------------------------------------------------" << endl;
	
}
short RandNum(int from , int to) {
	int ran = rand() % (to - from + 1) + from;
	return ran;
}
short Asker(short &num)

{
	cout << "Pls enter how many rounds you want to play: ";
	cin >> num;

	while (num > 100 || num < 1) {
		cout << "Please enter a number between 1 and 100: ";
		cin >> num;
	}

	return num;
}

short PlayerSelection(short Player) {
	cout << "Pls select : Rock[1] Paper[2] Scissor[3] : ";
	cin >> Player;
	if (Player <= 0 || Player > 3) {
		do {
			cout << "pls enter a number between 1 and 3 only : ";
			cin >> Player;
		} while (Player <= 0 || Player > 3);
		
	}
	return Player;
}
short ComputerSelection() {
	int computer = RandNum(1, 3);
	return computer;
}

string PlayerValue(RPS choice , short Player ,short PS ) {
	switch (PS)
	{
	case RPS::rock:
		return "Rock";
		break;
	case RPS::paper:
		return "Paper";
		break;
	case RPS::scissor:
		return "scissor";
		break;
	default:
		return "error";
		break;
	}
}
string ComputerValue(int CS) {
	switch (CS)
	{
	case RPS::rock:
		return "Rock";
		break;
	case RPS::paper:
		return "Paper";
		break;
	case RPS::scissor:
		return "scissor";
		break;
	default:
		return "error";
		break;
	}
}		  
											  
void PrintRoundCounterTab(short counter) {
	
		cout << "-------------------------------------------------------" << endl;
		cout << "                    Round Num : "<<counter<<"                " << endl;
		cout << "-------------------------------------------------------" << endl;
	
}
short PlayerChoice(short Player , RPS choice, short PS) {
	switch (PS)
	{
	case RPS::rock:
		cout << "Ur choice is: " << PlayerValue(choice, Player , PS) <<endl;
		return 1;
		break;						
	case RPS::paper:				
		cout << "Ur choice is: " << PlayerValue(choice, Player, PS) << endl;
		return 2;
		break;						
	case RPS::scissor:				
		cout << "Ur choice is: " << PlayerValue(choice, Player, PS) << endl;
		return 3;
		break;
	default:
		return 0;
		break;
	}
	

}
short ComputerChoice(int CS) {
	switch (CS)
	{
	case RPS::rock:
		cout << "Computer choice is: " << ComputerValue(CS) << endl;
		return 1;
		break;
	case RPS::paper:
		cout << "Computer choice is: " << ComputerValue(CS) << endl;
		return 2;
		break;
	case RPS::scissor:
		cout << "Computer choice is: " << ComputerValue(CS) << endl;
		return 3;
		break;
	default:
		return 0;
		break;
	}
}		  
											  
short RoundCompare(short Player, RPS choice , short PS , int CS) {
	int PC = PlayerChoice( Player , choice, PS);
	int CC = ComputerChoice(CS);
	if (PC == CC) {
		return 1;
	}
	else if (PC == 1 && CC == 2) {
		return 3;
	}
	else if (PC == 1 && CC == 3) {
		return 2;
	}
	else if (PC == 2 && CC == 1) {
		return 2;
	}
	else if (PC == 2 && CC == 3) {
		return 3;
	}
	else if (PC == 3 && CC == 1) {
		return 3;
	}
	else if (PC == 3 && CC == 2) {
		return 2;
	}
	
	else
		cout << "Error";
		return 0;
	
		
}

short PrintRoundWinnerWithEffects(short Player, RPS choice ,int PS , int CS) {
	short RC = RoundCompare(Player, choice, PS , CS);
	if (RC == 2) {
		cout << "Round winner is: Player" << endl;
		system("color 27");
		return 1;
	}
	else if (RC == 3) {
		cout << "Round winner is: computer" << endl;
		system("color 47");
		Beep(750, 300);
		return 2;
	}
	else if (RC == 1) {
		cout << "Round is: Draw" << endl;
		system("color 6F");
		return 3;
	}
	else
		cout << "error";
}

void PrintGameOverTab() {
	cout << "-------------------------------------------------------" << "\n" << endl;
	cout << "                       Game Over                       " << "\n" << endl;
	cout << "-------------------------------------------------------" << endl;

}
void ThanksTab() {
	cout << "-------------------------------------------------------" << endl;
	cout << "                  thank you for Playing                " << endl;
	cout << "-------------------------------------------------------" << endl;
}
string FinalWinner8Color(short Playercounter, short Computercounter, short Drawcounter) {
	if (Playercounter > Computercounter) {
		system("color 27");
		return "Player";
	}
	else if (Playercounter < Computercounter) {
		system("color 47");
		return "Computer";
	}
	else {
		system("color 6F");
		return "No Winner Draw";
	}
		
}
void GameResults(short num, short Playercounter, short Computercounter, short Drawcounter)
{
	cout << "---------------------[Game Results]--------------------" << endl;
	cout << "Game Roundes: " << num << endl;
	cout << "Player Win Times: " << Playercounter << endl;
	cout << "Computer Win Times: " << Computercounter << endl;
	cout << "Draw Times: " << Drawcounter << endl;
	cout << "Final Winner : " << FinalWinner8Color(Playercounter, Computercounter, Drawcounter) << endl;
	cout << "-------------------------------------------------------" << endl;
}

void RoundCounter(short &Playercounter, short &Computercounter, short &Drawcounter , short Player, short num , RPS choice ) {
	Playercounter = 0;
	Computercounter = 0;
	Drawcounter = 0;

	for (int A = 0; A < num; A++) {
		PrintRoundCounterTab(A+1);  
		short PS = PlayerSelection(Player);
		short CS = ComputerSelection();
		short PAATM = PrintRoundWinnerWithEffects(Player, choice, PS, CS); 
		if (PAATM == 1) {
			Playercounter += 1;
		}
		else if (PAATM == 2) {
			Computercounter += 1; 
		}
		else 
			Drawcounter += 1;
	}

	PrintGameOverTab();
	GameResults(num, Playercounter, Computercounter, Drawcounter);
}

char FullGame(short Playercounter, short Computercounter, short Drawcounter, short Player, short num, RPS choice, char AskRoundes) {
	system("color 0F");
	system("cls");
	Title();
	Asker(num);
	RoundCounter(Playercounter, Computercounter, Drawcounter, Player, num, choice);
	cout << "D u want to play more roundes?: Yes(Y) NO(N)";
	cin >> AskRoundes;
	while (AskRoundes != 'y' && AskRoundes != 'n') {
		cout << "Pls entr yes or no only: Yes(Y) NO(N)";
		cin >> AskRoundes;
	}
	if (AskRoundes == 'n') {
		ThanksTab();
		return 'n';
	}
	else
		return AskRoundes;
}
void PlayAgainAsker(short Playercounter, short Computercounter, short Drawcounter, short Player, short num, RPS choice , char AskRoundes) {
	char FG = FullGame(Playercounter, Computercounter, Drawcounter, Player, num, choice, AskRoundes);

	do {
		if (FG == 'n') {
			break;
		}
		FG = FullGame(Playercounter, Computercounter, Drawcounter, Player, num, choice, AskRoundes);
	} while (FG == 'y');
		
			
	
}





void StartGame() {
	srand((unsigned)time(0)); 
	short counter = 0;
	short num = 0;
	short Player = 0;
	short Playercounter = 0;
	short Computercounter = 0;
	short Drawcounter = 0;
	char AskRoundes = 'a';
	RPS choice = rock;
	PlayAgainAsker(Playercounter, Computercounter, Drawcounter, Player, num, choice , AskRoundes);
}

int main(){
	
	StartGame();
	return 0;
}