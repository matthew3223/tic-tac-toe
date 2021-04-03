import java.util.Scanner;
public class Main {
// This function creates a 3x3 board of 0s and returns it.
public static int [][] makeboard() {
   int [][] array = new int[3][3];
       for (int i = 0; i < array.length; i++) {
         for (int j = 0; j < array[i].length; j++) {
           array[i][j] = 0;
         }
       }
       return(array);
   }
// Takes in some 2D integer array, and prints it out in a neat format
public static void printboard(int [][] array) {
  for (int i = 0; i < array.length; i++) {
       String str = " ";
       for (int j = 0; j < array[i].length; j++) {
         str = str + array[i][j]+ " ";
       }
       System.out.println(str);
  }
}
// This function will take in a board, AND if that board has 3-in-a row of 1 or 2, THEN it will
// return true. Otherwise, it will return false.
public static boolean win(int[][] board) {
   int seenAOne = 0;
   int seenATwo = 0;
   // This will go through each row. If it sees 3-in-a-row, it'll return true
   for (int i = 0; i < board.length; i++) {
       seenAOne = 0;
       seenATwo = 0;
       for (int j = 0; j < board[i].length; j++) {
           if (board[i][j] == 1) {
               seenAOne++;
           } else if(board[i][j] == 2) {
               seenATwo++;
           }
       }
       if ((seenAOne == 3) || (seenATwo == 3)) {
           return(true);
       }
   }
   // This will go through each column. If it sees 3-in-a-row, it'll return true
   for (int j = 0; j < board.length; j++) {
       seenAOne = 0;
       seenATwo = 0;
       for (int i = 0; i < board.length; i++) {
           if (board[i][j] == 1) {
               seenAOne++;
           } else if(board[i][j] == 2) {
               seenATwo++;
           }
       }
       if ((seenAOne == 3) || (seenATwo == 3)) {
           return(true);
       }
   }
   //This will go through the diagonals. If it sees 3-in-a-row, it'll return true
   // Diagonal 1
   seenAOne = 0;
   seenATwo = 0;
   for (int i = 0; i < board.length; i++) {
       if (board[i][i] == 1) {
           seenAOne++;
       }
       if (board[i][i] == 2) {
           seenATwo++;
       }
   }
   if ((seenAOne == 3) || (seenATwo == 3)) {
       return(true);
   }
  
   // Diagonal 2
   seenAOne = 0;
   seenATwo = 0;
   for (int i = 0; i < board.length; i++) {
       if (board[i][board.length - 1 - i] == 1) {
           seenAOne++;
       }
       if (board[i][board.length - 1 - i] == 2) {
           seenATwo++;
       }
   }
   if ((seenAOne == 3) || (seenATwo == 3)) {
       return(true);
   }
  
   return(false);
}
// This function will determine if the board is full (i.e. if there are no 0s left on the board)
// If the board is full, it'll return true, otherwise it'll return false
public static boolean isBoardFull(int [][] board) {
   for (int i = 0; i < board.length; i++) {
       for (int j = 0; j < board[i].length; j++) {
           if (board[i][j] == 0) {
               return(false);
           }
       }
   }
   return(true);
}
// This function takes in a board, and a x,y coordinate pair, and a number, and changes the coordinate to that number on the board. 
public static int [][] changeBoard(int row, int col, int [][]theBoard, int valToAdd) {
   int [][] newBoard = theBoard;
   newBoard[row][col] = valToAdd;
   return(newBoard);
}
public static void main(String []args) {
   int [][] board = makeboard();
   printboard(board);            // Calling the function
  
   Scanner sc = new Scanner(System.in);
   int player = 0;
   int num = 0;
 
   while(!isBoardFull(board) && !win(board)) {
     if ((num % 2) == 1) {
       player = 2;
     } else if ((num % 2) == 0) {
       player = 1;
     }
    
     System.out.println("Player " + player + "'s turn");
 
     System.out.println("Enter a x and y coordinate separated by space");
     int a = sc.nextInt();
     int b = sc.nextInt();
    
     board = changeBoard(a, b, board, player);
     printboard(board);
     num++;
   }
}
}
