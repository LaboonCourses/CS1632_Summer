## Supplemental Rust Exercise

With a partner, develop a self-playing game I am calling "Tic-Tac-Schmoe" in Rust.  This game can be developed on your local computer or (mostly) by using the Rust playground at http://play.integer32.com.  You will not be able to enter user names using the Playground, so I recommend ensuring that it works on your computer; you will need to accept user input for Deliverable 7.  The game should meet the following functional requirements:

1. The user shall be asked to enter the names of twoplayers.  Both of these player's names shall be stored.  If there are any errors in entering their names, their names should be DEFAULT1 and DEFAULT2.
1. The first player entered plays as X and gets the first move.  The second player plays as O and gets the second move.
2. Each player chooses a random square to mark as an X or O (the first player will always enter X's and the second player will always enter O's).
3. Unlike normal tic-tac-toe, you may override other squares.  That is, if the first player has an X on a square, the second player may change it to an O.
3. You may also "waste" a move by writing over a square you already have marked with your own character.
3. After each iteration, print the board, with X indicated as 'X', O indicated as 'O', and Empty indicated as '.' (period).
3. After 100 iterations, the player with the most of their mark on the board (X or O) wins, and the other player loses.  If there is the same number, the game is tied.  Display who won, or if there was a tie, using the following formats:
  1. "*Player1* won!  *Player2* lost!"
  2. "*Player1* and *Player2* tied!"


It should follow some implementation requirements:

1. Printing the board should be in its own method which accepts a borrowed Board type and returns nothing.
1. Checking for a win should be in its own method which accepts a borrowed Board type and returns an enum GameStatus.
2. The tic-tac-toe board shall be a 3x3 array of Squares.  Note that the size of arrays in Rust is fixed at COMPILE time!
3. Have an enum Square which consists of three possible values: X, O, and Empty.
3. Have an enum GameStatus which consists of three possible values Player1Win and Player2Win.
3. The array shall be of type Square.
3. Use match instead of if statements whenever possible.  Trust me, your life will be easier!
4. There should be no compiler warnings or errors.
