#include<iostream>
using namespace std;

char space[3][3] = { {'1','2','3'}, {'4','5','6'}, {'7','8','9'} };
int row;
int column;
char token = 'x';
bool tie = false;
string n1 = " ";
string n2 = " ";

// Function to display the Tic Tac Toe board
void displayBoard() {
    cout << "        |        |" << endl;
    cout << "    " << space[0][0] << "   |    " << space[0][1] << "   |    " << space[0][2] << "  " << endl;
    cout << "        |        |" << endl;
    cout << "----------------------------" << endl;
    cout << "        |        |" << endl;
    cout << "    " << space[1][0] << "   |    " << space[1][1] << "   |    " << space[1][2] << " " << endl;
    cout << "        |        |" << endl;
    cout << "----------------------------" << endl;
    cout << "        |        |" << endl;
    cout << "    " << space[2][0] << "   |    " << space[2][1] << "   |    " << space[2][2] << " " << endl;
    cout << "        |        |" << endl;
}

// Function to get the player's move
void getPlayerMove() {
    int digit;
    if (token == 'x') {
        cout << n1 << ", please enter your move (1-9): ";
    }
    else {
        cout << n2 << ", please enter your move (1-9): ";
    }
    cin >> digit;

    // Validate the input
    if (digit >= 1 && digit <= 9) {
        row = (digit - 1) / 3;
        column = (digit - 1) % 3;
    }
    else {
        cout << "Invalid move. Please enter a number between 1 and 9." << endl;
        getPlayerMove(); // Ask again for a valid move
    }

    // Check if the chosen cell is already occupied
    if (space[row][column] == 'x' || space[row][column] == '0') {
        cout << "That cell is already occupied. Choose another one." << endl;
        getPlayerMove(); // Ask again for a valid move
    }
}

// Function to check the game's status
bool checkGameStatus() {
    // Check for a win in rows or columns
    for (int i = 0; i < 3; i++) {
        if (space[i][0] == space[i][1] && space[i][1] == space[i][2] ||
            space[0][i] == space[1][i] && space[1][i] == space[2][i]) {
            return true;
        }
    }

    // Check for a win in diagonals
    if (space[0][0] == space[1][1] && space[1][1] == space[2][2] ||
        space[0][2] == space[1][1] && space[1][1] == space[2][0]) {
        return true;
    }

    // Check for a tie
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (space[i][j] != 'x' && space[i][j] != '0') {
                return false;
            }
        }
    }
    
    tie = true;
    return false;
}

int main() {
    cout << "Enter the name of the first player: ";
    getline(cin, n1);

    cout << "Enter the name of the second player: ";
    getline(cin, n2);

    cout << endl;
    cout << "Player " << n1 << " will play first (x), and Player " << n2 << " will play second (0)." << endl;
    cout << endl;

    while (!checkGameStatus()) {
        displayBoard();
        getPlayerMove();
        space[row][column] = token;
        token = (token == 'x') ? '0' : 'x'; // Switch turns
    }

    displayBoard();

    if (tie) {
        cout << "It's a tie!" << endl;
    }
    else if (token == 'x') {
        cout << n2 << " wins!" << endl;
    }
    else {
        cout << n1 << " wins!" << endl;
    }

    return 0;
}

