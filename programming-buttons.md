# Programming the Buttons

## Setup

First update the import at the top of your file to include `Button`.

```py
from gpiozero import Button, LED
```

Near the top of your file, after you setup the LEDs and before the colour constants, setup your buttons with the pin numbers that you connected them to when building your circuit.

```py
red_button = Button(-1) # Change the pin number to match your circuit
blue_button = # Setup based on your circuit
yellow_button = # Setup based on your circuit
green_button = # Setup based on your circuit
```

## Running Code when the Buttons are Pressed

In order to run code when the buttons are pressed, copy the incomplete `button_pressed` and `button_released` functions below the `play_pattern` function.

```py
def button_pressed(button):
    # Code to respond to buttons being pressed goes here
```

```py
def button_released(button):
    # Code to respond to buttons being released goes here
```

Both of these functions require a single argument named `button` and will not return anything. To run these functions whenever the buttons are pressed and released, configure the GPIO library to call them. Below the `button_pressed` and `button_released` functions, add the following code **for each button**. For example, to configure the red button, use the following code.

```py
red_button.when_pressed = button_pressed
red_button.when_released = button_released
```

It is important to **reference the functions, but not call them** when configuring the GPIO library. You refer to the function by using it's name alone, without any parentheses or arguments. If you call the function, the GPIO library will be configured to run the _return value_ of the function when the button is pressed or released. This might cause an error when this line of your program runs, or your program may work without any errors, but it will not behave how you expect it to.

When correctly configured, the GPIO library will call the `button_pressed` and `button_released` functions with the button that was pressed as the argument whenever a button is pressed or released, respectively. For example, if the red button was pressed, `button_pressed` would run, and the value of it's argument would be equal to `red_button`.

## Responding to Button Presses

### Identifying the Button for each Colour

In order to identify what colour a button corresponds to, copy the incomplete `get_colour_for_button` below the `get_led_for_colour` function.

```py
def get_colour_for_button(button):
    # Code to return the colour for each button goes here
```

The `get_colour_for_button` requires a single argument named `button`. This function will take a button as an argument and return the integer colour value that the button corresponds to.

Implement the `get_colour_for_button` function. Remember that you defined the colour values when writing the pattern code.

### Lighting the LEDs

To respond to button presses, you must implement the incomplete `button_pressed` and `button_released` functions you created earlier.

When a button is pressed, the `button_pressed` function should

1. Light up the LED corresponding to the button that was pressed
2. Check if the button that was pressed matches the pattern

When a button is released, the `button_released` function should

1. Turn off the LED corresponding to the button that was released

Make `button_pressed` and `button_released` turn the corresponding LED on and off as described above. Don't worry about checking if the button matches the pattern yet; this is included in a later step.

## Testing

Before going further, make sure that your button code is working. Add the following code to the end of your file.

```py
while True:
    sleep(0.1)
```

Run your program and make sure that the corresponding LED lights up whenever you press the button, and goes out when you release it. Make sure to test all four buttons. If the buttons don't do what you expect them to, there may be a problem in your circuit or code. Identify and fix any problems, then run your program again to check if the problem has been fixed.

Delete this test code once you know the buttons are working correctly.