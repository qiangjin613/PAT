# PAT
算法小白的 PAT 参考指南

### Basic Level
语言：Java 8

### 范围
* int: 有符号[-2^31, 2^31-1] | [-2147483648, 2147483647] 10位，无符号[0, 2^32-1]
* long: 有符号[-2^63, 2^63-1] | [-9223372036854775808, 9223372036854775807] 19位

### 技巧
1. String -> char[]: 使用 `toCharArray()` 将字符串转换为 char[] 进行操作; 也可以使用 `charAt()` 来实现同样操作(推荐)
2. 针对有很多输入导致超时的时候，可以使用 BufferedReader 读取输入，并使用 `readLine()` 方法进行处理，可有效减少读取过慢和读取的参数异常问题（10^4 在 PAT 服务器大概需要 250ms；对于 10^4 输入一次输出 200ms 多次运行可能会AC）
3. StreamTokenizer 要比 BufferedReader 快一些（如题：`1063 计算谱半径 (20 分)`）
   ```java
   // BufferedReader 的报装不可以去掉，否则会影响 io 速度
   StreamTokenizer st = new StreamTokenizer(new BufferedReader(new InputStreamReader(System.in)));
   ``` 
4. 针对 Scanner 的 `nextXxxx()` 与 `nextLine()` 连用的情况，需要在两者之间添加 `nextLine()` 过滤掉将 `nextXxxx()` 的结束符过滤掉
5. 四舍五入与截断输出
   ```java
   System.out.printf("%+.2f", a); // 将 a 四舍五入保留两位小数并且带符号输出
   double a; System.out.print((a + 0.5)/10); // 对 int 型的 a 四舍五入输出
   douoble a; a = ((int)(a * 100)) / 100.0; // 对浮点数 a 保留 2 位小数（多余位数截取）
   ```
6. 对于在程序计算结束后进行输出并对各项输出进行特判的情况，可使用一个额外数组各项对计算结果进行标记，可大大简化编码复杂度
7. 对于输出：用指定大小的 StringBuilder 构建结果一次输出，要比在循环中输出多次结果要快一些（如：Basic Level 1017）
8. 对于输出：要求“行首尾不得有多余空格”，可以使用类似 `System.out.format("%s%d", flag? " ": "", i);` 解决
9. 对 ASCII 的秒用，如 `1033 旧键盘打字 (20 分)`
10. 类似于“排雷”、“跳棋”的地图中范围查找问题，详情查看 `1068 万绿丛中一点红 (20 分)`


### 有坑和需要注意的题目
#### Basic Level
|  题目   | 坑点  |
|  :----:  | ----  |
| 1051 复数乘法 (15 分) | `0.00` 和 `-0.00` 的输出 |
| 1081 检查密码 (15 分) | 密码的输入以回车结束，类似于 `fsdf 3278.fds d` 的密码输入，使用 `in.next()` 是不合理的 |
| 1012 数字分类 (20 分) | 对于输出结果要使用额外的数组进行标记，使用 `0` 或 `-1` 等在计算结果上进行标记都是会出错的。（如：使用 `0` 对结果标记时，针对输入 `2 11 11` 的样例，无法判断其计算结果为 `0` 还是该类数字（`n % 5 == 1`的情况）不存在） |
| 1017 A除以B (20 分) | 小心类似于 `3 5` 的输入样例，输出 `0 3` |
| 1032 挖掘机技术哪家强 (20 分) | 200ms、10^5 的输入量，对于 BufferedReader 是一个实现不了的任务 |
| 1052 卖个萌 (20 分) | 几乎搜遍全网题解，还是没能 AC，网传：测试样例包括非 ASCII 字符，PAT 上的 Java/Python 解释器无法正常读入这些 |
| 1057 数零壹 (20 分) | 一串长度未 10^5 的字符串勉强可以在 200ms 内完成，不过这需要多次提交，才能 AC |
| 1018 锤子剪刀布 (20 分) | 10^5 次的输入 200ms 最后一个测试点超时 |
| 1053 住房空置率 (20 分)、1063 计算谱半径 (20 分) | 使用 StreamTokenizer 可以 AC |
| 1058、1073 | 关于字符串统计的题对我来说是个 BUG |
| 1093 字符串A+B (20 分) | 合并字符串的一个比较好的方法：拼接、标记、合并 |