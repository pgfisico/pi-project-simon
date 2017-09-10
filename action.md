# Programming the Game

## Game Loop

In order to turn your LED and button code into a game, you must create a loop that the game runs in, as well as adding a check to see if the button pressed matches the pattern.

The basic structure of the game's loop will be to perform the following actions as long as the game has not been lost. The game is lost whenever the player presses the wrong button.

1. Add a random colour to the pattern
2. Play the pattern on the LEDs
3. Wait for the player to push all the buttons

To track if the game has been lost, add a variable named `game_lost` above `pattern` and set it to `False`

```py
game_lost = False
```

At the end of the file, create a loop that runs as long as `game_lost` is `False`. Then, add calls to the the `add_to_pattern` and `play_pattern` functions you wrote earlier inside the loop to perform the actions outlined above.

After and outside of the loop, add code to print that the game was lost.

## Checking Button Presses

In order to check if the button pressed matches the pattern, you need to keep track of the position in the pattern. Add the following variable just below your declaration of `pattern`.

```
pattern_position = 0
```

The `pattern_position` variable will be used to track how much of the pattern has been entered correctly using the buttons. In the `button_pressed` function, add code to do the following after turning the LED on.

1. If the colour in the pattern at `pattern_position` is not the same as the colour whose button was pressed, set `game_lost` to `True`.
2. Increment `pattern_position` by one

To change the value of `game_lost` and `pattern_position` in the `button_pressed` function, you will need to add the following line in `button_pressed` before you try changing the value of `game_lost` or `pattern_position`. This line tells the Python interpreter that you want to change the value of these variables instead of making a new variable with the same name that exists only in the `button_pressed` function.

```py
global game_lost, pattern_position
```

In the game loop you created earlier, add code which will reset `pattern_position` to zero every time a new colour is added to the pattern. This is so your program will start checking from the beginning of the pattern each time it is played. There is no need to use the `global` keyword to reset `pattern_position` because this code is not inside a function.

The last thing you need to do in the game loop is to wait until the wrong button is pressed or the whole pattern is entered correctly before ending the game or playing the next pattern, respectively. This can be accomplished by using the following code inside your game loop.

```py
while not game_lost and pattern_position < len(pattern):
    sleep(0.1)
```

This code waits a small amount of time as long as the game is not lost \(meaning a wrong button has not been pressed\), and `pattern_position` has not reached the last item in the `pattern` \(meaning the entire pattern has not been entered correctly yet\).

The`button_pressed`function is called by the GPIO library whenever a button is pressed, and you can imagine it as running at the same time as the loop above. The loop periodically checks if the `button_pressed` function has changed the value of `game_lost` or `pattern_position` to indicate that the program should end the game or add another colour to the pattern. The small sleep time allows other code, such as the `button_pressed` function, or programs on the Raspberry Pi to run while your code waits for `game_lost` or `pattern_position` to change.

`len` is a Python function which returns the number of items in `pattern`.

Finally at the end of your file, outside the game loop, print the message "You pressed the wrong button" to indicate the game was lost once the loop ends.

## Playing the Game

Run your program and see if it works as expected. If it doesn't do what you thought it would, identify and fix any problems, then run your program again to check if the problem has been fixed.

