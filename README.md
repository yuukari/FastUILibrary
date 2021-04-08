# FastUILibrary
UI library for BipOS (Amazfit Bip firmware mod)

## Features

+ Simple work with components using "getComponent..." and "setComponent..." methods:

  ```c
    Button* button = createButton();
    setButtonPosition(button, 16, 16);	
    setButtonSize(button, 144, 50);
    setButtonText(button, "Click me!");

    position buttonPosition = getButtonPosition(button);
  ```
+ Components supports event handling:
  ```c
    // Make function to handle button clicks
    void switch_click_handler(unsigned short enabled) {
      // Your awesome code
    }

    // In init function
    Switch* _switch = createSwitch();
    // Pass the pointer to click function
    setSwitchClickHandler(_switch, &switch_click_handler);
  ```

## List of components

+ Button component. Support click event handler

  ![Button](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Button.png)

+ Switch component. Support click event handler

  ![Switch](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/SwitchActive.png)

+ Checkbox component. Support click event handler

  ![Checkbox](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Checkbox.png)

+ Image component

  ![Image](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Image.png) 

+ Animation component. Supports methods for show next/prev frame, frame by index, and loop activation

  ![Animation](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Animation1.png) ![Animation](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Animation2.png) ![Animation](https://raw.githubusercontent.com/Yuukari/FastUILibrary/main/Images/Animation3.png)  

## Component lifecycle

For better understanding how works component lifecycle I recommend see [this repository](https://github.com/Yuukari/FastUIDemo), that demonstrates all components from library. You can use it as template for your application.

Here's a simple example for work with button component:

+ Creating button and setting initial parameters

  ```c
    Button* button = createButton();

    setButtonPosition(button, 16, 16);	
    setButtonSize(button, 144, 50);

    setButtonBackgroundColor(button, COLOR_BLUE);
    setButtonBorderColor(button, COLOR_AQUA);
    setButtonHoverColor(button, COLOR_YELLOW);
    setButtonText(button, "Button");

    setButtonClickHandler(button, &button_click_handler);

    app_data->button = button;
  ```
+ First render on watch screen
  ```c
    drawButton(app_data->button);
  ```
+ If user interact with screen, call function for handle gesture, and render component to show changes to user
  ```c
    gestureButton(app_data->button, gest);
    
    drawButton(app_data->button);
  ```
+ After some time we need to call update function. This will reset the active state of button (set border default color). After calling update function, we need to render component 
  ```c
    updateButton(app_data->button);
    
    drawButton(app_data->button);
  ```
+ Before exiting your app, you need to destroy all components that you create in init function
  ```c
    destroyButton(app_data->button);
  ```
