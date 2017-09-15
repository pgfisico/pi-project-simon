# Programming the Lights

## Setup

First create a new Python script named `simon.py`.

At the top of the file, import `LED` from the GPIO module. Below the import, setup your LEDs with the pin numbers that you connected them to when building your circuit.

```py
from gpiozero import LED

red_led = LED(0) # Change the pin number to match your circuit
blue_led = # Setup based on your circuit
yellow_led = # Setup based on your circuit
green_led = # Setup based on your circuit
```

## The Pattern

Start by creating an empty list to store the pattern. Add the following line below where you setup the LEDs.

```py
pattern = []
```

The items in the pattern list will need to correspond to a specific colour. In order to make it easier to pick a random colour, use a number to represent each colour. Using numbers allows you to pick a random colour using the `random` module in Python. The `random` module can be used to pick a random number, and you can use the numerical representations of the colours to turn the random number into a random colour.

In order to keep colours consistent throughout the program, add some constants above `pattern`. These will be the numbers you use to represent each colour in your program.

```py
RED = 1
BLUE = 2
YELLOW = 3
GREEN = 4
```

Next, create a function named `add_to_pattern` which requires no arguments below `pattern`. This function will add a random colour to the end of `pattern`.

To implement this function, you will need to know how to add to the end of a list. To add to the end of a list, use the list's `append` function. For example, the following would add the number `7` to the end of `pattern`.

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

After writing the code to create a random pattern, you will need code to play the pattern on the LEDs.

Below the `add_to_pattern` function, create a function named `play_pattern` which requires no arguments. This function should go through all of the colours in `pattern`, in order, and for each colour

1. Turn the appropriately coloured LED on
2. Turn the LED off after 0.42 seconds
3. Wait 0.05 seconds, to add a gap between each colour in the pattern

In order to follow these timings, recall the `sleep` function from the `time` module. To use it, add the following import to the top of your file.

```py
from time import sleep
```

In order to write the `play_pattern` function, you will need a way to know which LED to turn on. Above the `add_to_pattern` function, create a function named `get_led_for_colour` that requires a single argument named `colour`. This function will take the integer colour value from the pattern as an argument and return the corresponding LED. You will need to use the colour constants and LEDs you setup earlier to implement this function.

Implement both the `get_led_for_colour` and `play_pattern` functions as outlined above.

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

