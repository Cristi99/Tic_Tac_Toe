# Tic_Tac_Toe
A simple tic tac toe game.

package tictactoe;

import java.util.Scanner;

/**
 *
 * @author xrist
 */

public class TicTacToe
{
    
    public static void main(String[] args)
    {
        int i, j, cellstaken;
        cellstaken = 0; //  Everytime a cell gets filled in, the program will add 1 to cellstaken.
        
        String[][] gameboard = new String[3][3];
        Scanner in = new Scanner(System.in);
        String player = "X ";
        String winner = " ";
      
        //  Initializing the game board.
        
        for (i=0; i<3; i++)
        {
            for (j=0; j<3; j++)
            {
                gameboard[i][j] = "  ";
            }
        }
        
        GameBoardShow(gameboard);
       
        System.out.println("Ready? (Note: The rows and columns you choose must be 0-2)");
        
        while (winner.equals(" ") && cellstaken<9)
        {
            System.out.println("Player "+player+" choose a row and column:");
            
            int R, C;   //  R = row and C = column
            
            R = in.nextInt();
            C = in.nextInt();
            
            while (R<0 || R>3 || C<0 || C>3)
            {
                System.out.println("Please enter valid numbers.");
                R = in.nextInt();
                C = in.nextInt();
            }
           
            while (gameboard[R][C].equals("O ") || gameboard[R][C].equals("X "))
            {
                System.out.println("Cell taken. Please choose a new cell:");
                R = in.nextInt();
                C = in.nextInt();
            }
           
            gameboard[R][C] = player;
            cellstaken++;

            GameBoardShow(gameboard);

            if (player.equals("X "))
                player = "O ";
            else
                player = "X ";

            winner = CheckWinner(gameboard, winner);
        }
        
        if (winner.equals("X ") || winner.equals("O "))
            System.out.println("The winner is player "+winner+"!");
        else
            System.out.println("There is no winner. It's a draw!");
    }
    
    //  Creating the Tic Tac Toe board.
   
    static void GameBoardShow(String[][] gameboard)
    {
       System.out.println("/---|---|---\\");
       System.out.println("| "+gameboard[0][0]+"| "+gameboard[0][1]+"| "+gameboard[0][2]+"|");
       System.out.println("|---|---|---|");
       System.out.println("| "+gameboard[1][0]+"| "+gameboard[1][1]+"| "+gameboard[1][2]+"|");
       System.out.println("|---|---|---|");
       System.out.println("| "+gameboard[2][0]+"| "+gameboard[2][1]+"| "+gameboard[2][2]+"|");
       System.out.println("\\---|---|---/");
    }
    
    //  Checking if we have a winner yet.
    
    private static String CheckWinner(String[][] gameboard, String winner)
    {
        int cases;
        
        for (cases=0; cases<8; cases++)
        {
            String line = "";
            
            switch(cases)
            {
                case 0:
                    line = gameboard[0][0] + gameboard[1][1] + gameboard[2][2];
                break;
                
                case 1:
                    line = gameboard[0][0] + gameboard[0][1] + gameboard[0][2];
                break;
                
                case 2:
                    line = gameboard[1][0] + gameboard[1][1] + gameboard[1][2];
                break;
                
                case 3:
                    line = gameboard[2][0] + gameboard[2][1] + gameboard[2][2];
                break;
                
                case 4:
                    line = gameboard[0][0] + gameboard[1][0] + gameboard[2][0];
                break;
                
                case 5:
                    line = gameboard[0][1] + gameboard[1][1] + gameboard[2][1];
                break;
                
                case 6:
                    line = gameboard[0][2] + gameboard[1][2] + gameboard[2][2];
                break;
                
                case 7:
                    line = gameboard[0][2] + gameboard[1][1] + gameboard[2][0];
                break;
            }
            
            switch (line)
            {
                case "X X X ":
                    return "X ";
                case "O O O ":
                    return "O ";
            }
        }
        return " ";
    }
}
