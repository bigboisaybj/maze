# maze
import java.io.*;
import java.util.*;
import java.io.PrintWriter;

/**
 * Maze Game Class.
 *
 * INFO1103 Assignment 2, Semester 1, 2017.
 *
 * The Maze Game.
 * In this assignment you will be designing a maze game.
 * You will have a maze board and a player moving around the board.
 * The player can step left, right, up or down.
 * However, you need to complete the maze within a given number of steps.
 *
 * As in any maze, there are walls that you cannot move through. If you try to
 * move through a wall, you lose a life. You have a limited number of lives.
 * There is also gold on the board that you can collect if you move ontop of it.
 *
 * Please implement the methods provided, as some of the marks are allocated to
 * testing these methods directly.
 *
 * @author YOU :)
 * @date April, 2017
 *
 */
public class MazeGame {

	public static int Lives;
	public static int numberOfSteps;
	public static int startingGold;
	public static int numberOfRows;
	public static String[] board;
	public static int ycoordinate;
	public static int xcoordinate;

	/* You can put variables that you need throughout the class up here.
     * You MUST INITIALISE ALL of these class variables in your initialiseGame
     * method.
     */

    // A sample variable to show you can put variables here.
    // You would initialise it in initialiseGame method.
    // e.g. Have the following line in the initialiseGame method.
    // sampleVariable = 1;

    /**
     * Initialises the game from the given configuration file.
     * This includes the number of lives, the number of steps, the starting gold
     * and the board.
     *
     * If the configuration file name is "DEFAULT", load the default
     * game configuration.
     *
     * NOTE: Please also initialise all of your class variables.
     *
     * @args configFileName The name of the game configuration file to read from.
     * @throws IOException If there was an error reading in the game.
     *         For example, if the input file could not be found.
     */
    public static void initialiseGame(String configFileName) throws IOException {

		String fileName;
		
        if (configFileName.equals("DEFAULT")) {
			fileName = "DEFAULT";
			Lives = 3;
			numberOfSteps = 20;
			startingGold = 0;
			numberOfRows = 4;
			board = new String[numberOfRows];
			board[0] = "#@ ##  &4#";
			board[1] = "##  # ## #";
			board[2] = "###  3#   ";
			board[3] = "#######  #";
			
		/*for(int i = 0; i < numberOfRows;i++) {
			System.out.println(board[i]);
		}
		*/
		}
		else {
		File file1 = new File(configFileName);

		Scanner inputFile = new Scanner(file1);
		
		fileName = configFileName;
		Lives = inputFile.nextInt();
		numberOfSteps = inputFile.nextInt();
		startingGold = inputFile.nextInt();
		numberOfRows = inputFile.nextInt();
		String LineOne = inputFile.nextLine();
		board = new String[numberOfRows];

		for(int i = 0; i < numberOfRows;i++) {
			board[i] = inputFile.nextLine();
		}

		for(int i = 0; i < numberOfRows;i++) {
			System.out.println(board[i]);
		}
		inputFile.close();
		}
		// TODO: Implement this method.
    }
			

    /**
     * Save the current board to the given file name.
     * Note: save it in the same format as you read it in.
     * That is:
     *
     * <number of lives> <number of steps> <amount of gold> <number of rows on the board>
     * <BOARD>
     *
     * @args toFileName The name of the file to save the game configuration to.
     * @throws IOException If there was an error writing the game to the file.
     */
    public static void saveGame(String toFileName) throws IOException {
        // TODO: Implement this method.


   try {
     File file = new File("./" + toFileName); //print writer works on a file
     file.getParentFile().mkdirs();       //I don't know what this does, it just works


      PrintWriter writer = new PrintWriter(file);
			writer.println(Lives + " " + numberOfSteps + " " + startingGold + " " + numberOfRows);
			for (int f = 0; f < board.length; f++) {
				writer.println(board[f]);
			}
	   		writer.close();
		}
		catch (IOException e) {
			System.out.println("File not found");
		}
    }
    /**
     * Gets the current x position of the player.
     *
     * @return The players current x position.
     */
    public static int getCurrentXPosition() {
		xcoordinate = 0;
		ycoordinate = 0;
		int z = 0;
		int i = 0;
		char whereIsAnd = '0';
		for(i = 0; whereIsAnd != '&'; i++){

			for(z = 0; z < board[0].length(); z++) {
				whereIsAnd = board[i].charAt(z);
				if (whereIsAnd == '&') {
					break;
				}
			}
			if (whereIsAnd == '&') {
				break;
			}
		}
		xcoordinate = z;
		// TODO: Implement this method.
        return z;
    }

    /**
     * Gets the current y position of the player.
     *
     * @return The players current y position.
     */
    public static int getCurrentYPosition() {
        xcoordinate = 0;
		ycoordinate = 0;
		int z = 0;
		int i = 0;
		char whereIsAnd = '0';
		for(i = 0; i < numberOfRows; i++){
			for(z = 0; z < board[0].length(); z++) {
				whereIsAnd = board[i].charAt(z);
				if (whereIsAnd == '&') {
					break;
				}
			}
			if (whereIsAnd == '&') {
				break;
			}
		}
		ycoordinate = i;
		// TODO: Implement this method.
        return i;
    }

    /**
     * Gets the number of lives the player currently has.
     *
     * @return The number of lives the player currently has.
     */
    public static int numberOfLives() {
        return Lives;
    }

    /**
     * Gets the number of remaining steps that the player can use.
     *
     * @return The number of steps remaining in the game.
     */
    public static int numberOfStepsRemaining() {
        // TODO: Implement this method.
        return numberOfSteps;
    }

    /**
     * Gets the amount of gold that the player has collected so far.
     *
     * @return The amount of gold the player has collected so far.
     */
    public static int amountOfGold() {
        // TODO: Implement this method.
        return startingGold;
    }


    /**
     * Checks to see if the player has completed the maze.
     * The player has completed the maze if they have reached the destination.
     *
     * @return True if the player has completed the maze.
     */
    public static boolean isMazeCompleted() {
		if (board[ycoordinate].charAt(xcoordinate) == '@') {
			System.out.println("Congratulations! You completed the maze!");
		}
        // TODO: Implement this method.
        return false;
    }

    /**
     * Checks to see if it is the end of the game.
     * It is the end of the game if one of the following conditions is true:
     *  - There are no remaining steps.
     *  - The player has no lives.
     *  - The player has completed the maze.
     *
     * @return True if any one of the conditions that end the game is true.
     */
    public static boolean isGameEnd() {
		if (isMazeCompleted()) {
			return true;
		}
		if (numberOfSteps < 1) {
			System.out.println("Oh no! You have no steps left.");
			System.out.println("Better luck next time!");
			return true;
		}
		if (Lives < 1) {
			System.out.println("Oh no! You have no lives.");
			System.out.println("Better luck next time!");
			return true;
		}
		if ((numberOfSteps < 1) && (Lives < 1)) {
			System.out.println("Oh no! You have no lives and no steps left.");
			System.out.println("Better luck next time!");
			return true;
		}
		        // TODO: Implement this method.
        return false;
    }

    /**
     * Checks if the coordinates (x, y) are valid.
     * That is, if they are on the board.
     *
     * @args x The x coordinate.
     * @args y The y coordinate.
     * @return True if the given coordinates are valid (on the board),
     *         otherwise, false (the coordinates are out or range).
     */
    public static boolean isValidCoordinates(int x, int y) {
  //  isValidCoordinates METHOD
    boolean rt;

    // check y
    if(y > (board.length - 1) || y < 0){
      rt = false;
    }

    //check x
    else if(x > (board[0].length() - 1) || x < 0){
      rt = false;
    } else {
      rt = true;
    }
    return rt;
  }

    /**
     * Checks if a move to the given coordinates is valid.
     * A move is invalid if:
     *  - It is move to a coordinate off the board.
     *  - There is a wall at that coordinate.
     *  - The game is ended.
     *
     * @args x The x coordinate to move to.
     * @args y The y coordinate to move to.
     * @return True if the move is valid, otherwise false.
     */
    public static boolean canMoveTo(int x, int y) {

		if (board[y].charAt(x) == '#') {
			System.out.println("Invalid move. One life lost.");
			Lives -= 1;
			return false;
		}
		else if (!isValidCoordinates(x, y)) {
			System.out.println("Invalid move. One life lost.");
			Lives -= 1;
			return false;
		}
		else if (isGameEnd() == true) {
			return false;
		}
		// TODO: Implement this method.

        return true;
    }

    /**
     * Move the player to the given coordinates on the board.
     * After a successful move, it prints "Moved to (x, y)."
     * where (x, y) were the coordinates given.
     *
     * If there was gold at the position the player moved to,
     * the gold should be collected and the message "Plus n gold."
     * should also be printed, where n is the amount of gold collected.
     *
     * If it is an invalid move, a life is lost.
     * The method prints: "Invalid move. One life lost."
     *
     * @args x The x coordinate to move to.
     * @args y The y coordinate to move to.
     */
    public static void moveTo(int x, int y) {
      numberOfSteps -= 1;
try {
      char character = board[y].charAt(x);
      int CurrentX = getCurrentXPosition();
      int CurrentY = getCurrentYPosition();
	
      if (canMoveTo(x, y)){
        board[CurrentY] = board[CurrentY].substring(0, CurrentX) + "." + board[CurrentY].substring(CurrentX + 1);
        board[y] = board[y].substring(0, x) + "&" + board[y].substring(x + 1);
		  if (character >= 49 && character <= 160) {
		  System.out.printf("Moved to (%d, %d).\n", CurrentX, CurrentY);
          System.out.printf("Plus %c gold.\n", character);
          startingGold += Character.getNumericValue(character);
		  }
      	else if (!(character >= 48 && character <= 16)) {
		System.out.printf("Moved to (%d, %d).\n", CurrentX, CurrentY);
		}
      }
	}
		catch (ArrayIndexOutOfBoundsException et) {
			System.out.println("Invalid move. One life lost.");
			Lives -= 1;
		}
	/*else  if (!canMoveTo(x, y)) {
		Lives -= 1;
	}
	*/	

      /*
	  if (character >= 49 && character <= 160) {
		  System.out.printf("Moved to (%d, %d).\n", CurrentX, CurrentY);
          System.out.printf("Plus %c gold.\n", character);
          startingGold += Character.getNumericValue(character);
		  */
    }
	public static void getShow() {
		System.out.println(getCurrentXPosition());
		System.out.println(getCurrentYPosition());
	}

    /**
     * Prints out the help message.
     */
    public static void printHelp() {
       System.out.println("Usage: You can type one of the following commands.");
		System.out.println("help         Print this help message.");
		System.out.println("board        Print the current board.");
		System.out.println("status       Print the current status.");
		System.out.println("left         Move the player 1 square to the left.");
		System.out.println("right        Move the player 1 square to the right.");
		System.out.println("up           Move the player 1 square up.");
		System.out.println("down         Move the player 1 square down.");
		System.out.println("save <file>  Save the current game configuration to the given file.");
		// TODO: Implement this method.
    }

    /**
     * Prints out the status message.
     */
    public static void printStatus() {
        System.out.printf("Number of live(s): %d\n", Lives);
		System.out.printf("Number of step(s) remaining: %d\n", numberOfSteps);
		System.out.printf("Amount of gold: %d\n", startingGold);
		// TODO: Implement this method.
    }

    /**
     * Prints out the board.
     */
    public static void printBoard() {
       for(int i = 0; i < numberOfRows;i++) {
			System.out.println(board[i]);
			}
		// TODO: Implement this method.
		/*String[] firstLine = {"#", "@", " ", "#", "#", " ", "&", "4", "#"};

		for(int i=0; i<9; i++) {
			System.out.print(firstLine[i]);
		}*/

    }

    /**
     * Performs the given action by calling the appropriate helper methods.
     * [For example, calling the printHelp() method if the action is "help".]
     *
     * The valid actions are "help", "board", "status", "left", "right",
     * "up", "down", and "save".
     * [Note: The actions are case insensitive.]
     * If it is not a valid action, an IllegalArgumentException should be thrown.
     *
     * @args action The action we are performing.
     * @throws IllegalArgumentException If the action given isn't one of the
     *         allowed actions.
     */
    public static void performAction(String action) throws IllegalArgumentException {
		
	try {	
      String[] arrayResponse = action.toLowerCase().split("\\s+"); //the save function is multiple words, put it into an array

      action = action.toLowerCase();

      if ( action.equals("help")){
  			printHelp();
  		}
  		else if (action.equals("board")) {
  			printBoard();
  		}
  		else if ( action.equals("status")) {
  			printStatus();
  		}
  		else if ( action.equals("left")) {
  			moveTo((getCurrentXPosition() -1),getCurrentYPosition());
  		}
  		else if ( action.equals("right")) {
  			moveTo((getCurrentXPosition() +1),getCurrentYPosition());
  		}
  		else if ( action.equals("up")) {
  			moveTo(getCurrentXPosition(),(getCurrentYPosition() - 1));
  		}
  		else if ( action.equals("down")) {
  			moveTo(getCurrentXPosition(),(getCurrentYPosition() + 1));
  		}
		else if ( action.equals("show")) {
  			getShow();
  		}
  		else if (arrayResponse[0].equals("save")) {
        saveGame(arrayResponse[1]);
		}
		else {
			throw new IllegalArgumentException("fail");
		}
	}
		
       catch (IOException e){
        System.out.println("'Error: Could not load the game configuration from 'does_not_exist.txt'");
      }
  		// TODO: Implement this method.
      }

    /**
     * The main method of your program.
     *
     * @args args[0] The game configuration file from which to initialise the
     *       maze game. If it is DEFAULT, load the default configuration.
     */
    public static void main(String[] args) {

  		Scanner keyboard = new Scanner(System.in);
		
  try {
  		if (args.length < 1) {
  			System.out.printf("Error: Too few arguments given. Expected 1 argument, found 0.\n Usage: MazeGame [<%s>|DEFAULT]", args[0]);
  			return;
  		} else if (args.length > 1) {
  			System.out.println("Error: Too many arguments given. Expected 1 argument, found " + args.length + ".");
  			System.out.println("Usage: MazeGame [<game configuration file>|DEFAULT]");
  			return;
  		}
  				initialiseGame(args[0]);

  					while(keyboard.hasNextLine()) {
  						String userResponse = keyboard.nextLine();

  					if (isGameEnd() == true) {
  						return;
  					}
  					performAction(userResponse);

  				}
	  		System.out.println("You did not complete the game.");
  }
			catch (IllegalArgumentException ex) {
				System.out.println("You did not complete the game.");
  			} 
			catch(IOException e){
				System.out.println("Error: Could not load the game configuration from 'does_not_exist.txt'.");
			}
		}
        // Run your program (reading in from args etc) from here.
    }
