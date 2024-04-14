
Hi!

I wrote a few files to debug SE lab directly through VS code's inbuilt debugger, as it helps see what code's running and makes it easier to debug. 

If you would like to use it, download the zip file below and copy the entire uncompressed folder to the root directory of your repository. 

Here's what the directory should look like once you paste in the folder:

![[Pasted image 20240413222920.png]]

From there, if you press the Run and Debug icon on the left of your VS Code window (or press CMD/CTRL + Shift + D), the debug panel will show up. On the top of that panel, click the dropdown next to the green play button and it should let you select what debug task to run. After that, just click the green play button and it should run your code. 

Here's what the run and debug panel should look like:

![[Pasted image 20240413225901.png]]

There's three different options to run:
1. Launch SE w/ Testcase (this will ask for the path to the testcase you want to run, and where to save checkpoint output)
2. Launch Instructor SE w/ Testcase (this will ask for which week's instructor ref to run,  the path to the testcase to run, and where to save checkpoint output)
	-  This one won't actually let you debug anything, but it just makes it easier to run the instructor output without having to keep copying/pasting the command
3. Test SE by Week (this will ask what week's test cases to run) (also won't let you debug)

The output will show up in the `TERMINAL` tab in VS code as a new terminal. To pass commands into GDB, click `DEBUG CONSOLE` and type in `-exec {command(s)}` (ex. `-exec print W_out`), though most values you need will show up in the Debug Panel on the left. (Also, hovering over values in the current method you're in will let you see the values of them).

The first two will save the checkpoint output to a file. By default, it's set to `my_sol.txt` for 1, and `instr_sol.txt` for 2. You can change these either in the `launch.json` file or by changing it in the input prompt when running the testcase.

Here's VS Code's guide to debugging C/C++: https://code.visualstudio.com/docs/cpp/cpp-debug.

Here's an example of what your VS Code should look like when debugging with breakpoints:

![[Screenshot 2024-04-13 at 10.53.55 PM.png]]

Btw: if you download the file and unzip it and it disappears, it's because your OS might think it's a hidden file, just make sure hidden files are viewable.

Hope this helps! If you have any problems with it lmkc