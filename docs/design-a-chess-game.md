# 设计一款象棋游戏

> 原文:[https://www.geeksforgeeks.org/design-a-chess-game/](https://www.geeksforgeeks.org/design-a-chess-game/)

**问题陈述**:问题是使用面向对象的原理设计一款[棋局](https://en.wikipedia.org/wiki/Chess)。

**问 In:** Adobe、亚马逊、微软等。

**解答:**
面试时会问这类问题，来判断应聘者的面向对象设计技能。所以，首先我们应该考虑班级。

主要课程包括:

1.  **点:**一个点代表 8×8 网格中的一个块和一个可选块。
2.  **棋子:**系统的基本积木，每一个棋子都会被放置在一个点上。片类是一个抽象类。扩展类(卒、王、皇后、车、骑士、主教)实现抽象操作。
3.  **棋盘:**棋盘是一套 8×8 的盒子，里面装着所有的活动棋子。
4.  **玩家:**玩家类代表玩游戏的参与者之一。
5.  **移动:**代表游戏移动，包含起点和终点。移动类也将跟踪移动的玩家。
6.  **Game:** This class controls the flow of a game. It keeps track of all the game moves, which player has the current turn, and the final result of the game.

    我们来看看细节。这些代码是不言自明的。你可以看看不同类的属性/变量和方法。

    **点:**代表棋盘上的一个单元格:

    ```
    public class Spot {
        private Piece piece;
        private int x;
        private int y;

        public Spot(int x, int y, Piece piece)
        {
            this.setPiece(piece);
            this.setX(x);
            this.setY(y);
        }

        public Piece getPiece()
        {
            return this.piece;
        }

        public void setPiece(Piece p)
        {
            this.piece = p;
        }

        public int getX()
        {
            return this.x;
        }

        public void setX(int x)
        {
            this.x = x;
        }

        public int getY()
        {
            return this.y;
        }

        public void setY(int y)
        {
            this.y = y;
        }
    }
    ```

    **棋子:**表示所有棋子共同功能的抽象类:

    ```
    public abstract class Piece {

        private boolean killed = false;
        private boolean white = false;

        public Piece(boolean white)
        {
            this.setWhite(white);
        }

        public boolean isWhite()
        {
            return this.white;
        }

        public void setWhite(boolean white)
        {
            this.white = white;
        }

        public boolean isKilled()
        {
            return this.killed;
        }

        public void setKilled(boolean killed)
        {
            this.killed = killed;
        }

        public abstract boolean canMove(Board board, 
                                     Spot start, Spot end);
    }
    ```

    **王者:**代表王者为棋子:

    ```
    public class King extends Piece {
        private boolean castlingDone = false;

        public King(boolean white)
        {
            super(white);
        }

        public boolean isCastlingDone()
        {
            return this.castlingDone;
        }

        public void setCastlingDone(boolean castlingDone)
        {
            this.castlingDone = castlingDone;
        }

        @Override
        public boolean canMove(Board board, Spot start, Spot end)
        {
            // we can't move the piece to a Spot that 
            // has a piece of the same color
            if (end.getPiece().isWhite() == this.isWhite()) {
                return false;
            }

            int x = Math.abs(start.getX() - end.getX());
            int y = Math.abs(start.getY() - end.getY());
            if (x + y == 1) {
                // check if this move will not result in the king
                // being attacked if so return true
                return true;
            }

            return this.isValidCastling(board, start, end);
        }

        private boolean isValidCastling(Board board, 
                                         Spot start, Spot end)
        {

            if (this.isCastlingDone()) {
                return false;
            }

            // Logic for returning true or false
        }

        public boolean isCastlingMove(Spot start, Spot end)
        {
            // check if the starting and 
            // ending position are correct
        }
    }
    ```

    **骑士:**代表骑士为棋子

    ```
    public class Knight extends Piece {
        public Knight(boolean white)
        {
            super(white);
        }

        @Override
        public boolean canMove(Board board, Spot start, 
                                                Spot end)
        {
            // we can't move the piece to a spot that has
            // a piece of the same colour
            if (end.getPiece().isWhite() == this.isWhite()) {
                return false;
            }

            int x = Math.abs(start.getX() - end.getX());
            int y = Math.abs(start.getY() - end.getY());
            return x * y == 2;
        }
    }
    ```

    同样，我们可以为其他棋子创建职业，如**女王**、**棋子**、**车**、**主教**等。

    **棋盘:**代表一个棋盘:

    ```
    public class Board {
        Spot[][] boxes;

        public Board()
        {
            this.resetBoard();
        }

        public Spot getBox(int x, int y)
        {

            if (x < 0 || x > 7 || y < 0 || y > 7) {
                throw new Exception("Index out of bound");
            }

            return boxes[x][y];
        }

        public void resetBoard()
        {
            // initialize white pieces
            boxes[0][0] = new Spot(0, 0, new Rook(true));
            boxes[0][1] = new Spot(0, 1, new Knight(true));
            boxes[0][2] = new Spot(0, 2, new Bishop(true));
            //...
            boxes[1][0] = new Spot(1, 0, new Pawn(true));
            boxes[1][1] = new Spot(1, 1, new Pawn(true));
            //...

            // initialize black pieces
            boxes[7][0] = new Spot(7, 0, new Rook(false));
            boxes[7][1] = new Spot(7, 1, new Knight(false));
            boxes[7][2] = new Spot(7, 2, new Bishop(false));
            //...
            boxes[6][0] = new Spot(6, 0, new Pawn(false));
            boxes[6][1] = new Spot(6, 1, new Pawn(false));
            //...

            // initialize remaining boxes without any piece
            for (int i = 2; i < 6; i++) {
                for (int j = 0; j < 8; j++) {
                    boxes[i][j] = new Spot(i, j, null);
                }
            }
        }
    }
    ```

    **玩家:**玩家的抽象类，可以是人，也可以是电脑。

    ```
    public abstract class Player {
        public boolean whiteSide;
        public boolean humanPlayer;

        public boolean isWhiteSide()
        {
            return this.whiteSide;
        }
        public boolean isHumanPlayer()
        {
            return this.humanPlayer;
        }
    }

    public class HumanPlayer extends Player {

        public HumanPlayer(boolean whiteSide)
        {
            this.whiteSide = whiteSide;
            this.humanPlayer = true;
        }
    }

    public class ComputerPlayer extends Player {

        public ComputerPlayer(boolean whiteSide)
        {
            this.whiteSide = whiteSide;
            this.humanPlayer = false;
        }
    }
    ```

    **棋步:**要表示棋步:

    ```
    public class Move {
        private Player player;
        private Spot start;
        private Spot end;
        private Piece pieceMoved;
        private Piece pieceKilled;
        private boolean castlingMove = false;

        public Move(Player player, Spot start, Spot end)
        {
            this.player = player;
            this.start = start;
            this.end = end;
            this.pieceMoved = start.getPiece();
        }

        public boolean isCastlingMove()
        {
            return this.castlingMove;
        }

        public void setCastlingMove(boolean castlingMove)
        {
            this.castlingMove = castlingMove;
        }
    }
    ```

    ```
    public enum GameStatus {
        ACTIVE,
        BLACK_WIN,
        WHITE_WIN,
        FORFEIT,
        STALEMATE,
        RESIGNATION
    }
    ```

    **游戏:**要代表一种象棋游戏:

    ```
    public class Game {
        private Player[] players;
        private Board board;
        private Player currentTurn;
        private GameStatus status;
        private List<Move> movesPlayed;

        private void initialize(Player p1, Player p2)
        {
            players[0] = p1;
            players[1] = p2;

            board.resetBoard();

            if (p1.isWhiteSide()) {
                this.currentTurn = p1;
            }
            else {
                this.currentTurn = p2;
            }

            movesPlayed.clear();
        }

        public boolean isEnd()
        {
            return this.getStatus() != GameStatus.ACTIVE;
        }

        public boolean getStatus()
        {
            return this.status;
        }

        public void setStatus(GameStatus status)
        {
            this.status = status;
        }

        public boolean playerMove(Player player, int startX, 
                                    int startY, int endX, int endY)
        {
            Spot startBox = board.getBox(startX, startY);
            Spot endBox = board.getBox(startY, endY);
            Move move = new Move(player, startBox, endBox);
            return this.makeMove(move, player);
        }

        private boolean makeMove(Move move, Player player)
        {
            Piece sourcePiece = move.getStart().getPiece();
            if (sourcePiece == null) {
                return false;
            }

            // valid player
            if (player != currentTurn) {
                return false;
            }

            if (sourcePiece.isWhite() != player.isWhiteSide()) {
                return false;
            }

            // valid move?
            if (!sourcePiece.canMove(board, move.getStart(), 
                                                move.getEnd())) {
                return false;
            }

            // kill?
            Piece destPiece = move.getStart().getPiece();
            if (destPiece != null) {
                destPiece.setKilled(true);
                move.setPieceKilled(destPiece);
            }

            // castling?
            if (sourcePiece != null && sourcePiece instanceof King
                && sourcePiece.isCastlingMove()) {
                move.setCastlingMove(true);
            }

            // store the move
            movesPlayed.add(move);

            // move piece from the stat box to end box
            move.getEnd().setPiece(move.getStart().getPiece());
            move.getStart.setPiece(null);

            if (destPiece != null && destPiece instanceof King) {
                if (player.isWhiteSide()) {
                    this.setStatus(GameStatus.WHITE_WIN);
                }
                else {
                    this.setStatus(GameStatus.BLACK_WIN);
                }
            }

            // set the current turn to the other player
            if (this.currentTurn == players[0]) {
                this.currentTurn = players[1];
            }
            else {
                this.currentTurn = players[0];
            }

            return true;
        }
    }
    ```

    **参考:**http://massivethinchterview . blogspot . com/2015/07/design-chess-game-use-oo-principles . html