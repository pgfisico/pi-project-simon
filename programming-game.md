# Programming the Game

## Game Loop

In order to turn your LED and button code into a game, you must create a loop that the game runs in, and add a check to see if the button pressed matches the pattern.

The basic structure of the game's loop will be to perform the following actions as long as the game has not been lost. The game is lost whenever the player presses the wrong button.

1. Add a random colour to the pattern
2. Play the pattern on the LEDs
3. Wait for the player to push the buttons in the pattern

To track if the game has been lost, add a variable named `game_lost` above `pattern` and set it to `False`.

```py
game_lost = False
```

At the end of the file, create a loop that runs as long as `game_lost` is `False`. Then, add calls to the functions you wrote earlier inside the loop to perform the first two actions actions outlined above.

## Checking Button Presses

In order to check if the button pressed matches the pattern, you need to keep track of how much of the pattern the player has entered. Add the following variable just below your declaration of `pattern`.

```
pattern_position = 0
```

The `pattern_position` variable will be used to track how much of the pattern has been entered correctly using the buttons.

### Accessing Items in a List

To access items in a list, you can refer to them using an index. The index is a numerical value that represents an item's position in the list. The illustration of the `fruits` list below shows three fruits in the list and their index below them. Note that the index for the first item in the list, "apple", is zero. This is why you have set `pattern_position` to zero, so it refers to the first item in the list. The list has three items in it, and this can be checked by using the `len` function. Using the `len` function on `fruits` would return 3, as shown below the list. Note that because the first item in the list has index zero, the last item has an index equal to the length of the list minus one.

![](/assets/List Indexing.png)

To access an item in the list using it's index, place the index in square brackets after the name of the list. For example, both of the following pieces of code will store the value "banana" in the variable `favourite_fruit`.

```py
fruits = ['apple', 'banana', 'orange']
favourite_fruit = fruits[1]
```

```py
fruits = ['apple', 'banana', 'orange']
index = 1
favourite_fruit = fruits[index]
```

### Comparing the Button Press Against the Pattern

In the `button_pressed` function, add code to do the following after turning the LED on.

1. If the colour in the pattern at `pattern_position` is not the same as the colour whose button was pressed, set `game_lost` to `True`.
2. Increment `pattern_position` by one

To change the value of `game_lost` and `pattern_position` in the `button_pressed` function, you will need to add the following line in `button_pressed` before you try changing the value of `game_lost` or `pattern_position`. This line tells the Python interpreter that you want to change the value of these variables instead of making a new variable with the same name that exists only in the `button_pressed` function.

```py
global game_lost, pattern_position
```

In the game loop you created earlier, add code which will reset `pattern_position` to zero every time a new colour is added to the pattern. This is so your program will start checking from the beginning of the pattern each time it is played. There is no need to use the `global` keyword before resetting `pattern_position` inside the game loop because this code is not inside a function.

The last thing you need to do in the game loop is to wait until the wrong button is pressed or the whole pattern is entered correctly before ending the game or playing the next pattern, respectively. This can be accomplished by using the following code inside your game loop.

```py
while not game_lost and pattern_position < len(pattern):
    sleep(0.1)
```

This code waits a small amount of time as long as the game is not lost \(meaning a wrong button has not been pressed\), and `pattern_position` has not reached the last item in the `pattern` \(meaning the entire pattern has not been entered correctly yet\).

If you're wondering how the above code works, recall that the `button_pressed` function is called by the GPIO library whenever a button is pressed, and you can imagine it as running at the same time as the loop above. The loop periodically checks if the `button_pressed` function has changed the value of `game_lost` or `pattern_position` to indicate that the program should end the game or add another colour to the pattern. The small sleep time allows other code, such as the `button_pressed` function or other programs on the Raspberry Pi, to run while your code waits for `game_lost` or `pattern_position` to change. The comparison of `pattern_position` to the length of the `pattern` works due to the way list indexing works, as explained earlier.

Finally at the end of your file, outside the game loop, print the message "You pressed the wrong button" to indicate the game was lost once the loop ends.

## Playing the Game

Run your program and see if it works as expected. If it doesn't do what you thought it would, identify and fix any problems, then run your program again to check if the problem has been fixed.

Once it's working, play the game to see how long a pattern you can remember!