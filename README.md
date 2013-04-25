#nonogram-solver!

Title is self-explanatory: code for a nonogram-solving program. Only for single-colored puzzles.

##How it works!
###Overview
The puzzle is broken up into a series of lines, 1 for each row and 1 for each column, which are all handled separately. The reasoning behind this is that the solution for a line is not directly dependent of any others: simply of the number and length of its blocks and of the information already gathered about it. Since each row and column pair have 1 cell in common, this means that a 

###Stacks
####
The source code defines a stack structure, along with an interface for interacting with said structure. The need for this arose out of a simple concept: the more information we have on a line, the more information we're likely to get.

Imagine we are solving a row and discover that it's 4th cell must be FULL. This cell that we've identified is also part of a perpendicular column: the 4th column to be precise. This means we have uncovered new information on the 4th column, and thus if we re-examine it, we are likely to be able to uncover even more information! Here's a graphic example:

Let's take a simple premise: say that the program starts by solving the 4th column, followed by the 1st, and then it starts solving lines from the stack, and as it identifies each cell it pushes its perpendicular line onto the stack of lines that should be solved.

 0 1 2 0
0
0
1
2

We start solving the 4th column: the solution to it is instantaneous.

 0 1 2 0
0      -
0      -
1      -
2      -

So the perpendicular rows were added to the stack, the 4th one being last. Before using the stack, the program still solves the 1st column, by hypothesis:

 0 1 2 0
0-     -
0-     -
1-     -
2-     -

Once again the rows are added to the stack, the 4th one being last once more. Now the program uses the stack: we solve the 4th row.

 0 1 2 0
0-     -
0-     -
1-     -
2- # # -

The fact that we had identified 2 cells in this row made it so that we could identify the remaining 2. This is a loose example, but it's basically common sense that what is being proposed is true.




####Did it have to be a stack?
No, in fact the first thing that occured to me was a FIFO list, but after manually solving a few puzzles following the described logic, it appeared that stacks were always better than FIFO. This most likely (read: definitely) depends on the puzzle itself, but stacks have the added benefit of being a tiny bit simpler (only need to track the top).

####Possible developments

