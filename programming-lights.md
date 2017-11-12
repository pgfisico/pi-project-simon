# Programming the Lights

## Setup

Create a new Python script named `simon.py`.

At the top of the file, import `LED` from the GPIO module. Below the import, setup your LEDs with the pin numbers that you connected them to when building your circuit.

```py
from gpiozero import LED

red_led = LED(0) # Change the pin number to match your circuit
blue_led = LED(0) # Change the pin number to match your circuit
yellow_led = LED(0) # Change the pin number to match your circuit
green_led = LED(0) # Change the pin number to match your circuit
```

## The Pattern

Start by creating an empty list to store the pattern that will be played on the LEDs. Add the following line below where you setup the LEDs.

```py
pattern = []
```

The items in the pattern list will need to represent a specific colour. In order to make it easier to pick a random colour, use a number to represent each colour. Using numbers allows you to pick a random colour using the `random` module in Python. The `random` module can be used to pick a random number, and you can use the numerical representations of the colours to turn the random number into a random colour.

In order to keep colours consistent throughout the program, add some constants above `pattern`. These will be the numbers you use to represent each colour in your program.

```py
RED = 1
BLUE = 2
YELLOW = 3
GREEN = 4
```

Next, copy the incomplete `add_to_pattern` function below `pattern`. This function requires no arguments and will not return anything.

```py
def add_to_pattern():
    # Code to add a random colour to the end of the pattern goes here
```

This `add_to_pattern` function should add a random colour to the end of `pattern`. To implement this function, you will need to know how to add to the end of a list. To add to the end of a list, use the list's `append` function. For example, the following would add the number `7` to the end of `pattern`.

```py
pattern.append(7)
```

In order to pick a random colour, use the random module. At the top of your file, add the following import.

```py
from random import randint
```

The `randint` function can be used to generate a random integer. The random module's documentation provides the following description of `randint`.

> `random.randint(a, b)`
>
> Return a random integer `N` such that `a <= N <= b`. Alias for `randrange(a, b + 1)`.

You will need to pick values of `a` and `b` that ensure the random integer that `randint` returns matches one of the colour constants created earlier.

Now that you know how to add to the end of a list and generate random numbers, implement the `add_to_pattern` function.

## Lighting the LEDs in a Pattern

### Identifying the LED for each Colour

In order to play the pattern on the LEDs, you will need a way to know which LED to turn on for each numeric value in `pattern`. To do this, copy the incomplete `get_led_for_colour` function below the `add_to_pattern` function.

```py
def get_led_for_colour(colour):
    # Code to return the LED for each colour goes here
```

The `get_led_for_colour` requires a single argument named `colour` and will return the LED that corresponds to that colour. The `colour` argument will be a number equal to one of the colour constants you added earlier. The function should return the corresponding LED. For example, if `colour` is equal to `RED`, the function should return `red_led`.

To return a value from a function, use the `return` keyword. For example, the following function always returns 12.

```py
def get_number():
    return 12
```

Implement the `get_led_for_colour` function, making sure it will work for all four colours.

### Lighting the LEDs

In order to play the randomly generated pattern on the LEDs, copy the incomplete `play_pattern` function below the `add_to_pattern` function. The `play_pattern` function requires no arguments and will not return anything.

```py
def play_pattern():
    for colour in pattern:
        # Code to turn the appropriate LED on and off goes here
        #
        # The variable colour will contain the numerical colour value
        # for the LED that needs to be turned on and off
```

The `play_pattern` function should go through all of the colours in the `pattern` list, in order, and for each colour

1. Turn the appropriately coloured LED on
2. Turn the LED off after 0.42 seconds
3. Wait 0.05 seconds, to add a gap between each colour in the pattern

The incomplete version of the function above already contains a loop which goes through every colour in the pattern. You must add code inside the loop to turn the appropriate LED on and off.

To determine which LED corresponds to the numerical colour value, use the `get_led_for_colour` function you implemented earlier.

To follow the LED on and off timings, recall the `sleep` function from the `time` module. To use it, add the following import to the top of your file.

```py
from time import sleep
```

Implement the `play_pattern` function as outlined above.

## Testing

Before going further, make sure that your pattern and LED code is working. Add the following code to the end of your file.

```py
while True:
    add_to_pattern()
    play_pattern()
    sleep(2)
```

Run your program and make sure that the LEDs are flashing in a pattern, and that each time the pattern plays it has a new colour at the end. If the LEDs don't do what you expect them to, there may be a problem in your circuit or code. Identify and fix any problems, then run your program again to check if the problem has been fixed.

Delete this test code once you know the LEDs are working correctly.