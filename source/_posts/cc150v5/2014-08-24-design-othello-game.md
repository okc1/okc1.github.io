---
layout: post
title: "[CC150v5] 8.8 Design Othello Game "
comments: true
category: CC150v5

---

### Question

> Othello is played as follows: Each Othello piece is white on one side and black on the other. When a piece is surrounded by its opponents on both the left and right sides, or both the top and bottom, it is said to be captured and its color is flipped. 

> The win is assigned to the person with the most pieces. Implement the object-oriented design for Othello. 

### Class

1. Game
	1. Two Player objects
	1. a board object
	1. singleton class (unless otherwise specified, this needs to be discussed)
1. Board
	1. Keep the score (black/white count). Of course we can put score in Game Class as well, it seems logically related to the board a bit more. 
	1. Array of Piece objects
	1. getScore() method
1. Piece
	1. stores color info
	1. flip() function
1. Player
	1. stores color info
	1. playPiece() method
1. Color Enum
1. Direction Enum

### Functions 

1. placePiece() by the Player (which triggers the following 2 methods)
1. private flipSection(Position fromWhere, Color c, Direction up/down/left/right) by the board
1. private updateScore() by the board
1. getScore() by the board

#### Follow up: Do we need separate Board and Game classes?

Strictly speaking, no. The drawback is adding an extra layers. A function that calls Game class is immediately calling Board class. 

But keeping the objects separate allows us to have a logical separation between the board (which contains just logic involving placing pieces) and the game (which involves times, game flow, etc.). 

### Conclusion

This is an easy, and very standard OOD question. Keep the logic clear, design the layers and object hierarchy, and the rest of things will come naturally. 

### Code 

Game.java

    public class Game {
        private Player[] players;
        private static Game instance;
        private Board board;
        private final int ROWS = 10;
        private final int COLUMNS = 10;

        private Game() {
            board = new Board(ROWS, COLUMNS);
            players = new Player[2];
            players[0] = new Player(Color.Black);
            players[1] = new Player(Color.White);
            Automator.getInstance().initialize(players); // used for testing
        }

        public static Game getInstance() {
            if (instance == null) {
                instance = new Game();
            }
            return instance;
        }

        public Board getBoard() {
            return board;
        }
    }

Board.java

    public class Board {
        private int blackCount = 0;
        private int whiteCount = 0;
        private Piece[][] board;

        public Board(int rows, int columns) {
            board = new Piece[rows][columns];
        }

        public void initialize() {
            /* initial board has a grid like the following in the center:
             *     WB
             *     BW
             */
            int middleRow = board.length / 2;
            int middleColumn = board[middleRow].length / 2;
            board[middleRow][middleColumn] = new Piece(Color.White);
            board[middleRow + 1][middleColumn] = new Piece(Color.Black);
            board[middleRow + 1][middleColumn + 1] = new Piece(Color.White);
            board[middleRow][middleColumn + 1] = new Piece(Color.Black);
            blackCount = 2;
            whiteCount = 2;
        }

        public boolean placeColor(int row, int column, Color color) {
            if (board[row][column] != null) {
                return false;
            }

            /* attempt to flip each of the four directions */
            int[] results = new int[4];
            results[0] = flipSection(row - 1, column, color, Direction.up);
            results[1] = flipSection(row + 1, column, color, Direction.down);
            results[2] = flipSection(row, column + 1, color, Direction.right);
            results[3] = flipSection(row, column - 1, color, Direction.left);

            /* compute how many pieces were flipped */
            int flipped = 0;
            for (int result : results) {
                if (result > 0) {
                    flipped += result;
                }
            }

            /* if nothing was flipped, then it's an invalid move */
            if (flipped < 0) {
                return false;
            }

            /* flip the piece, and update the score */
            board[row][column] = new Piece(color);
            updateScore(color, flipped + 1);
            return true;
        }

        private int flipSection(int row, int column, Color color, Direction d) {
            /* Compute the delta for the row and the column. At all times, only the row or the column
             * will have a delta, since we're only moving in one direction at a time.
             */
            int r = 0;
            int c = 0;
            switch (d) {
            case up:
                r = -1;
                break;
            case down:
                r = 1;
                break;
            case left:
                c = -1;
                break;
            case right:
                c = 1;
                break;
            }

            /* If out of bounds, or nothing to flip, return an error (-1) */
            if (row < 0 || row >= board.length || column < 0 || column >= board[row].length || board[row][column] == null) {
                return -1;
            }

            /* Found same color - return nothing flipped */
            if (board[row][column].getColor() == color) {
                return 0;
            }

            /* Recursively flip the remainder of the row. If -1 is returned, then we know we hit the boundary
             * of the row (or a null piece) before we found our own color, so there's nothing to flip. Return
             * the error code.
             */
            int flipped = flipSection(row + r, column + c, color, d);
            if (flipped < 0) {
                return -1;
            }

            /* flip our own color */
            board[row][column].flip();
            return flipped + 1;
        }

        public int getScoreForColor(Color c) {
            if (c == Color.Black) {
                return blackCount;
            } else {
                return whiteCount;
            }
        }

        private void updateScore(Color newColor, int newPieces) {
            /* If we added x pieces of a color, then we actually removed x - 1 pieces of the other
             * color. The -1 is because one of the new pieces was the just-placed one.
             */
            if (newColor == Color.Black) {
                whiteCount -= newPieces - 1;
                blackCount += newPieces;
            } else {
                blackCount -= newPieces - 1;			
                whiteCount += newPieces;
            }
        }

        public void printBoard() {
            for (int r = 0; r < board.length; r++) {
                for (int c = 0; c < board[r].length; c++) {
                    if (board[r][c] == null) {
                        System.out.print("_");
                    } else if (board[r][c].getColor() == Color.White) {
                        System.out.print("W");
                    } else {
                        System.out.print("B");
                    }
                }
                System.out.println();
            }
        }
    }

Player.java

    public class Player {
        private Color color;
        public Player(Color c) {
            color = c;
        }

        public int getScore() {
            return Game.getInstance().getBoard().getScoreForColor(color);
        }

        public boolean playPiece(int row, int column) {
            return Game.getInstance().getBoard().placeColor(row, column, color);
        }

        public Color getColor() {
            return color;
        }
    }
