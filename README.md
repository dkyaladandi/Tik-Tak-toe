package tiktaktoe;

import java.util.Scanner;

public class tiktaktoe {

    public static void main(String[] args) {
        char[] board = { '1', '2', '3', '4', '5', '6', '7', '8', '9' };

        int numberOfSquaresPlayed = 0;
        char whoseTurnItIs = 'x';
        String gameEndingMessage = "";

        while (numberOfSquaresPlayed < 9) {
            printTheBoard(board);
            getTheUserToSelectTheirSquare(board, whoseTurnItIs);

            numberOfSquaresPlayed++; // Move this up to avoid miscount in draw

            if (theyWonTheGame(board, whoseTurnItIs)) {
                gameEndingMessage = "Player '" + whoseTurnItIs + "' won! Congratulations!";
                break;
            } else if (numberOfSquaresPlayed == 9) {
                gameEndingMessage = "It's a draw!";
            } else {
                whoseTurnItIs = (whoseTurnItIs == 'x') ? 'o' : 'x';
            }
        }

        printTheBoard(board);
        System.out.println(gameEndingMessage);
    }

    private static void printTheBoard(char[] board) {
        System.out.printf("%n %s | %s | %s %n", board[0], board[1], board[2]);
        System.out.println("---+---+---");
        System.out.printf(" %s | %s | %s %n", board[3], board[4], board[5]);
        System.out.println("---+---+---");
        System.out.printf(" %s | %s | %s %n%n", board[6], board[7], board[8]);
    }

    private static void getTheUserToSelectTheirSquare(char[] board, char whoseTurnItIs) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            try {
                System.out.printf("Player %s, choose an available square (1-9): ", whoseTurnItIs);
                int input = scanner.nextInt();

                if (input < 1 || input > 9) {
                    System.out.println("Please choose a number between 1 and 9.");
                    continue;
                }

                if (Character.isDigit(board[input - 1])) {
                    board[input - 1] = whoseTurnItIs;
                    break;
                } else {
                    System.out.println("Sorry, that square is already taken.");
                }
            } catch (Exception e) {
                System.out.println("Invalid input. Please enter a number between 1 and 9.");
                scanner.next(); // clear buffer
            }
        }
    }

    private static boolean theyWonTheGame(char[] board, char player) {
        // winning combinations
        return (board[0] == player && board[1] == player && board[2] == player) || // row 1
               (board[3] == player && board[4] == player && board[5] == player) || // row 2
               (board[6] == player && board[7] == player && board[8] == player) || // row 3
               (board[0] == player && board[3] == player && board[6] == player) || // column 1
               (board[1] == player && board[4] == player && board[7] == player) || // column 2
               (board[2] == player && board[5] == player && board[8] == player) || // column 3
               (board[0] == player && board[4] == player && board[8] == player) || // diagonal
               (board[2] == player && board[4] == player && board[6] == player);   // diagonal
    }
}

