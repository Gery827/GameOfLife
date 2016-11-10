# SlowLifeGUI
Conway's Game of Life, in GUI Form.  Deliberately non-performant.

To profile the system, after opening the origin, I made the 9 (3*3) cells in the center
alive, then click “Run” button for 10 times, “write”, then “undo” for 10 times, then
“Load” one time, then I clicked “Run Continous”.

Based on the sampler’s result, some of the hottest spots of the program are
“MainPanel.convertToInt()”, “Cell.toString()”, “MainPanel. runContinuous()” and
“MainPanel.backup()”.

Therefore, I tried to change 4 methods. The first is convertToInt(), which is
consuming a lot of CPU, and most of the methods are nothing useful. The toString()
method is similar to this one, which has some useless code in it. Testing the
toString() method is easy, but the convertToInt() method is a private method.
Therefore, other classes cannot access it. However, it would be miserable to test
this method manually, since it’s not easy to see the result. To try to test the private
method, I googled about how to do it and learned about using mirror and test the
method successfully.

For the runContinuous() and backup() method, there is no obvious way to use unit
test, therefore, I had to use manual test and both of the test passed.

Manual 1: For runContinuous() method:
Precondition: Make the center 3*3 cells alive and click “Run” for 10 times
Execution: Click “runContinuous”
Postcondition: Everything works just fine

Manual 2: For “backup()” method:
(Precondition: Make the center 3*3 cells alive and click “Run” for 10 times
Execution: Click “undo”
Postcondition: The world is returned to its previous situation
Run TestGUI.java
