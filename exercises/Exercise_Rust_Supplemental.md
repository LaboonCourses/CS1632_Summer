## Supplemental Rust Exercise

With a partner, develop a tic-tac-toe game in Rust, using the following functional requirements:

1. The player shall be asked to enter their name and this name shall be stored.
1. The player plays as X and gets the first move.
1. The player enters their moves in the format 0,2.
1. If the entered move is not in the format n,n where n > 0 and n < 2, then display "Invalid move entered".
1. If the entered move is not an empty square, then display "That square is already marked".
2. The computer chooses a random free square to mark as an O.
3. If the computer or player wins, then display "Computer wins!" or "*Player* wins" respectively, display statistics (see below) and exit.  In the latter case, *Player* should be replaced by the user's name (entered earlier).
4. If there is a tie (no valid moves left), then display "Tie!", display statistics (see below), and exit.

It should follow some implementation requirements:

1. Validation of moves should be in a separate method.  That is, have a method which accepts the move as a String and returns a Result indicating the move.
2. The tic-tac-toe board shall be a 3x3 array.  Note that the size of arrays in Rust is fixed at COMPILE time!
3. Have an enum Square which consists of three possible values: X, O, and Empty.
3. The array shall be of type Square.
3. Use match instead of if statements whenever possible.
4. There should be no compiler warnings or errors.