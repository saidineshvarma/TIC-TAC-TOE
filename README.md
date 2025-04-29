# TIC-TAC-TOE
import java.util.Scanner;
public class TicTacToe {
    private char[][] board;
    private char currentPlayer;
    public TicTacToe() {
        board = new char[4][4];
        currentPlayer = 'X';
        initializeBoard();
    }
    private void initializeBoard()
    {
        for (int i = 1; i < 4; i++)
        {
            for (int j = 1; j < 4; j++)
            {
                board[i][j] = '-';
            }
        }
    }
    private void printBoard()
    {
        for (int i = 1; i < 4; i++)
        {
            for (int j = 1; j < 4; j++) 
            {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }
    private boolean isValidMove(int row, int col)
    {
        return row >= 1 && row < 4 && col >= 1 && col < 4 && board[row][col] == '-';
    }
    private boolean makeMove(int row, int col) 
    {
        if (isValidMove(row, col))
        {
            board[row][col] = currentPlayer;
            return true;
        }
        return false;
    }
    private boolean checkWin() 
    {
        for (int i = 1; i < 4; i++)
        {
            if (board[i][1] == currentPlayer && board[i][2] == currentPlayer && board[i][3] == currentPlayer) {
                return true;
            }
            if (board[1][i] == currentPlayer && board[2][i] == currentPlayer && board[3][i] == currentPlayer) {
                return true;
            }
        }
        if ((board[1][1] == currentPlayer && board[2][2] == currentPlayer && board[3][3] == currentPlayer) ||
                (board[1][3] == currentPlayer && board[2][2] == currentPlayer && board[3][1] == currentPlayer)) 
                {
            return true;
        }
        return false;
    }
    private boolean isBoardFull() 
    {
        for (int i = 1; i < 4; i++)
        {
            for (int j = 1; j < 4; j++) 
            {
                if (board[i][j] == '-')
                {
                    return false;
                }
            }
        }
        return true;
    }
    public void playGame()
    {
        Scanner scanner = new Scanner(System.in);
        while (true)
        {
            printBoard();
            System.out.println("Player " + currentPlayer + "'s turn. Enter row and column (1-3):");
            int row = scanner.nextInt();
            int col = scanner.nextInt();
            if (makeMove(row, col))
            {
                if (checkWin())
                {
                    printBoard();
                    System.out.println("Player " + currentPlayer + " wins!");
                    break;
                } 
                else if (isBoardFull())
                {
                    printBoard();
                    System.out.println("It's a draw!");
                    break;
                }
                currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
            }
            else 
            {
                System.out.println("Invalid move, try again.");
            }
        }
    }
    public static void main(String[] args) {
        TicTacToe game = new TicTacToe();
        game.playGame();
    }
}
