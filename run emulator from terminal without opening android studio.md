## Problem
It's very time and resource consuming to open the android studio app and then run the emulator from there to run the react-native app on it. But you don't have to do that, you can run the emulator from the terminal very easily.

## Solution

Open your terminal and run the following command to see the available emulators.

```
emulator -list-avds
```

You will get the list of the avds availble like `Pixel_4_XL_API_30`

Next run the following command to run the emulator

```
emulator -avd Pixel_4_XL_API_30
```

This will run the emulator

<img width="462" alt="image" src="https://user-images.githubusercontent.com/11868557/206152019-13b750a4-cd85-4ee5-94af-c0a8db739135.png">