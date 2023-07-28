# Project 0

assignment中直接说明了：`tilt` will take you 3 to 10 hours to complete



row: 排，行

Column: 纵列



### 1. 2048的得分原理：

Each time two tiles merge to form a larger tile, the player earns a number of points on the new tile.

The “Max Score” is the maximum score the user has achieved in that game session. It isn’t updated until the game is over, so that is why it remains 0 throughout the animated GIF example.

### 2. 程序设计思路

Model-View-Controller Pattern (MVC), and Observe Pattern.

The MVC pattern divides our problem into three parts:

- The **model** represents the subject matter being represented and acted upon – in this case incorporating the state of a board game and the rules by which it may be modified. Our model resides in the `Model`, `Side`, `Board`, and `Tile` classes. The instance variables of `Model` fully determine what the state of the game is. Note: You’ll only be modifying the `Model` class.
- A **view** of the model, which displays the game state to the user. Our view resides in the `GUI` and `BoardWidget` classes.
- A **controller** for the game, which translates user actions into operations on the model. Our controller resides mainly in the `Game` class, although it also uses the GUI class to read keystrokes.

### 3. 题目的解读

tile就是每个方格，使用`tile.value()`来获取tile的数字



side代表的是方向，可以使用`Side s = Side.NORTH`(这里不需要使用new)

可以直接使用`public static void printSide(Side.NORTH)`



This class represents the board of tiles itself. It has three methods that you’ll use: `setViewingPerspective`, `tile`, `move`. Optionally, for experimentation, you can use `getRandomNonNullTile`.

### 4. 问题点

guiding里面说要使用java 15但是截图里面用的是14.0.2，我用的全部都是15（动图里面用的15），没有问题

### 5. 前三个都相当简单，掠过

### 6. tilt

> Computer science is essentially about one thing: Managing complexity. Writing the `tilt` method is a rich experience that will give you a chance to try just that. 

side的一长串解释看上去有点难以理解：解决这个问题背后的想法是，通过使用下面的col()和row()方法从重定向转换到标准坐标，可以安排使用完全相同的代码来计算向任何特定方向倾斜棋盘的结果。

> 还是看不懂

Tile t = board.tile(1, 2); board.move(1, 3, t); t = board.tile(1, 0); board.move(1, 2, t);