# C-#include <iostream>
#include <vector>

using namespace std;

class TicTacToe {
private:
    vector<vector<char>> board;
    char currentPlayer;

public:
    TicTacToe() : board(3, vector<char>(3, ' ')), currentPlayer('X') {}

    void displayBoard() {
        cout << "\nCurrent Board:\n";
        for (int i = 0; i < 3; ++i) {
            for (int j = 0; j < 3; ++j) {
                cout << board[i][j];
                if (j < 2) cout << " | ";
            }
            cout << endl;
            if (i < 2) cout << "---------\n";
        }
    }

    bool placeMark(int row, int col) {
        if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
            board[row][col] = currentPlayer;
            return true;
        }
        return false;
    }

    bool checkWin() {
        // Check rows and columns
        for (int i = 0; i < 3; ++i) {
            if ((board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) ||
                (board[0][i] == currentPlayer && board[1][i] == currentPlayer && board[2][i] == currentPlayer)) {
                return true;
            }
        }
        // Check diagonals
        if ((board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) ||
            (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)) {
            return true;
        }
        return false;
    }

    bool checkDraw() {
        for (const auto& row : board) {
            for (char cell : row) {
                if (cell == ' ') return false;
            }
        }
        return true;
    }

    void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    void playGame() {
        int row, col;
        while (true) {
            displayBoard();
            cout << "Player " << currentPlayer << ", enter your move (row and column): ";
            cin >> row >> col;

            if (placeMark(row - 1, col - 1)) {
                if (checkWin()) {
                    displayBoard();
                    cout << "Player " << currentPlayer << " wins!\n";
                    break;
                } else if (checkDraw()) {
                    displayBoard();
                    cout << "It's a draw!\n";
                    break;
                }
                switchPlayer();
            } else {
                cout << "This move is not valid. Try again.\n";
            }
        }
    }
};

int main() {
    TicTacToe game;
    game.playGame();
    return 0;
}
