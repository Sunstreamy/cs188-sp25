
### **`pacman.py` 命令行选项详解**

#### **通用选项**

*   **`-h, --help`**
    *   **作用：** 显示这个帮助信息并退出程序。
    *   **用法：** `python pacman.py -h`
    *   **说明：** 当你不确定某个命令怎么用时，这是你的第一个求助工具。

---

#### **游戏设置**

*   **`-n GAMES, --numGames=GAMES`**
    *   **作用：** 指定要连续玩多少局游戏。
    *   **默认值：** 1
    *   **用法：** `python pacman.py -n 5` (玩 5 局游戏)
    *   **说明：** 主要用于需要多次运行来评估智能体平均表现的场景（比如在有随机性的游戏中）。

*   **`-l LAYOUT_FILE, --layout=LAYOUT_FILE`**
    *   **作用：** 从指定的布局文件加载地图。布局文件通常在 `layouts` 文件夹下。
    *   **默认值：** `mediumClassic`
    *   **用法：** `python pacman.py -l tinyMaze` (加载 `tinyMaze.lay` 地图)
    *   **说明：** 这是你在这个项目中**最常用**的选项之一，用来切换不同的测试迷宫。

*   **`-p TYPE, --pacman=TYPE`**
    *   **作用：** 指定使用哪个“智能体 (Agent)”来控制 Pacman。智能体的代码通常在 `pacmanAgents.py` 或 `searchAgents.py` 中定义。
    *   **默认值：** `KeyboardAgent` (由你用键盘控制)
    *   **用法：** `python pacman.py -p SearchAgent` (使用 `SearchAgent` 来控制 Pacman)
    *   **说明：** 这是另一个**最常用**的选项，用来测试你编写的不同 AI 智能体。

*   **`-g TYPE, --ghosts=TYPE`**
    *   **作用：** 指定使用哪个智能体来控制幽灵。
    *   **默认值：** `RandomGhost` (随机移动的幽灵)
    *   **用法：** `python pacman.py -g DirectionalGhost` (使用会朝 Pacman 移动的幽灵)
    *   **说明：** 在后面的项目中，当你需要处理更智能的对手时会用到。

*   **`-k NUMGHOSTS, --numghosts=NUMGHOSTS`**
    *   **作用：** 指定游戏中最多使用多少个幽灵。
    *   **默认值：** 4
    *   **用法：** `python pacman.py -k 2` (只使用 2 个幽灵)
    *   **说明：** 用于调整游戏难度。

---

#### **显示与图形**

*   **`-t, --textGraphics`**
    *   **作用：** 只使用 ASCII 字符在终端中显示游戏画面，不弹出图形窗口。
    *   **用法：** `python pacman.py -t`
    *   **说明：** 当你在没有图形界面的环境（比如通过 SSH 连接到服务器）中运行代码时非常有用。

*   **`-q, --quietTextGraphics`**
    *   **作用：** 生成最少的文本输出，并且不显示图形。
    *   **用法：** `python pacman.py -q`
    *   **说明：** 主要用于自动评分器，因为它只关心最终结果，不关心中间过程。

*   **`-z ZOOM, --zoom=ZOOM`**
    *   **作用：** 缩放图形窗口的大小。大于 1 是放大，小于 1 是缩小。
    *   **默认值：** 1.0
    *   **用法：** `python pacman.py -l bigMaze -z 0.5` (将窗口缩小到 50%)
    *   **说明：** 在处理大地图时非常有用，可以让你看全整个迷宫。

*   **`--frameTime=FRAMETIME`**
    *   **作用：** 设置两帧画面之间的时间延迟（单位是秒）。值越小，游戏速度越快。
    *   **默认值：** 0.1
    *   **用法：** `python pacman.py --frameTime 0.5` (让游戏变得很慢)
    *   **说明：** 用于调试，方便你观察 Pacman 的每一步移动。

---

#### **调试与高级功能**

*   **`-f, --fixRandomSeed`**
    *   **作用：** 固定随机数种子。
    *   **用法：** `python pacman.py -f`
    *   **说明：** 确保每次运行游戏时，所有随机事件（比如幽灵的初始移动）都是完全一样的。这对于复现和调试 Bug 非常重要。

*   **`-r, --recordActions`**
    *   **作用：** 将游戏过程（主要是动作序列）记录到一个文件中。
    *   **用法：** `python pacman.py -r`
    *   **说明：** 用于保存精彩的游戏对局或需要分析的失败案例。

*   **`--replay=GAMETOREPLAY`**
    *   **作用：** 回放一个之前录制好的游戏文件。
    *   **用法：** `python pacman.py --replay my_game_record.pickle`
    *   **说明：** 用于复盘和分析。

*   **`-a AGENTARGS, --agentArgs=AGENTARGS`**
    *   **作用：** 向你指定的智能体（通过 `-p` 选项）传递参数。
    *   **默认值：** 无
    *   **用法：** `python pacman.py -p SearchAgent -a fn=bfs,prob=CornersProblem`
    *   **说明：** 这是项目中**极其重要**的选项！它让你可以在不修改代码的情况下，告诉 `SearchAgent` 应该使用哪个搜索函数 (`fn=bfs`) 和哪个搜索问题 (`prob=CornersProblem`)。参数之间用逗号分隔。

*   **`-c, --catchExceptions`**
    *   **作用：** 开启异常处理和超时机制。
    *   **用法：** `python pacman.py -c`
    *   **说明：** 这是一个**伪装成暂停功能的调试选项**。在 CS188 的这个项目中，当游戏正常结束时，这个选项会捕获 "game over" 信号，并**暂停程序，等待用户按键**。**所以，`--catchExceptions` 或 `-c` 就是你之前问的“如何让窗口不自动关闭”的答案！**

*   **`--timeout=TIMEOUT`**
    *   **作用：** 设置一个智能体在单局游戏中计算所能花费的最长时间（单位是秒）。
    *   **默认值：** 30
    *   **用法：** `python pacman.py --timeout 10`
    *   **说明：** 自动评分器用它来防止你的代码因为死循环或效率太低而无限运行下去。

---

#### **训练 (主要用于后面的项目)**

*   **`-x NUMTRAINING, --numTraining=NUMTRAINING`**
    *   **作用：** 指定有多少局游戏是用于“训练”的，在训练期间会抑制图形输出以加快速度。
    *   **默认值：** 0
    *   **用法：** `python pacman.py -p QLearningAgent -x 100` (先静默训练 100 局)
    *   **说明：** 在后面的强化学习项目中会用到，用于训练智能体。

希望这个详细的列表能帮助你更好地利用 `pacman.py` 这个强大的工具！