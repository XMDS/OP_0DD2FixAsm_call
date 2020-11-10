# OP_0DD2FixAsm_call  
## English  
### what is this ?  
`0DD2FixAsm_call`is a CLEO script for Android GTA. It fixes the problem of calling function of Android CLEO opcode 0DD2. You can now call functions with more than 4 parameters. Now, when you write cleo, you can use R4 to set the fifth parameter, and so on, you can use up to R49, and a total of 50 parameter settings (R0--R49) are supported.
This cleo supports any version of Android GTASA/GTAVC/GTA3 games.  

### Detailed description(Please be sure to read)
When writing an Android CLEO script, if you need to call a function to complete some functions, there will be the following code:

    30@ = A function
    Suppose the function has 4 parameters
    0@ = The first parameter
    1@ = The second parameter
    2@ = The third parameter
    3@ = The fourth parameter

    0DD3: context_set_reg 3 value 3@ // 4
    0DD3: context_set_reg 2 value 2@ // 3
    0DD3: context_set_reg 1 value 1@ // 2
    0DD3: context_set_reg 0 value 0@ // 1
    0DD2: context_call_func 30@  //func
    0DD4: 31@ = context_get_reg 0 //return value
Before calling a function in Android CLEO, first use the opcode 0DD3 to set the parameters of the function, and then use 0DD2 to call the function. If you need the return value of the function, you can use 0DD4 to get the return value of the function at the end.  
Among them, the reg in 0DD3 and 0DD4 represents the register, `reg 0` represents the R0 register, and so on.  
According to the ARM standard, when calling a function, R0-R3 is usually used to pass in and set function parameters, and R0 sends out the function return value.  
For functions with more than 4 parameters, the first 4 parameters are still passed in R0-R3, while other parameters are passed in the stack.
However, [AlexanderBlade](https://gtaforums.com/profile/182287-alexander-blade/) did not implement stack transfer parameters for the 0DD2 opcode when making [Android CLEOLibrary](https://gtaforums.com/topic/663125-android-cleo-android/). This led us to call functions in Android cleo scripts, only to call functions with parameters less than or equal to 4, and for parameters greater than 4 functions. After we call, the following parameters are invalid. Before that, we can only call functions with parameters less than or equal to 4.  
Now the cleo script `0DD2FixAsm_call` rewrites the code of `Asm_call` and injects it into the 0DD2 opcode of Libcleo.so. And solved the problem.

### Help and installation
You can download this cleo here, it is open source.
It also contains two test scripts(GTASA):   
[box_hello world](https://github.com/XMDS/OP_0DD2FixAsm_call/blob/master/source/Test%20script/box_hello%20world.txt)(10 seconds after entering the game, the black box in the upper left corner shows "hello world")  
[draw_shadow](https://github.com/XMDS/OP_0DD2FixAsm_call/blob/master/source/Test%20script/draw_shadow.txt)(A purple halo is created under the player’s feet)  

If your cleo needs to call a function with more than 4 parameters, you must use my cleo script to support the game. Even if you don't use a multi-parameter function, it can run perfectly in the game without affecting the game.  
I suggest that when writing and publishing your cleo, please write a description and attach my cleo script.
