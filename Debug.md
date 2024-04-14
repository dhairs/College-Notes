
Hi!

I wrote a few files to debug SE lab directly through VS code's inbuilt debugger, as it helps see what code's running and makes it easier to debug. 

If you would like to use it, download the zip file below and copy it to the root directory of your repository. 

From there, if you press the Run and Debug icon on the left of your VS Code window (or press CMD/CTRL + Shift + D), the debug window will show up. On the top of that, click the dropdown next to the green play button and it should let you select what debug task to run. 

There's three different options to run:
1. Launch SE w/ Testcase (when you run this, it'll ask for the path to the testcase you want to run)
2. Launch Instructor SE w/ Testcase (this will ask for which week's instructor ref to run, as well as the path to the testcase to run)
3. Test SE by Week (this will ask what week's test cases to run)

The first two will save the checkpoint output to a file. By default, it's set to `my_sol.txt` for 1, and `instr_sol.txt` for 2. You can change these either in the `launch.json` file or by changing it in the input prompt when running the testcase.