##一些注意点

- 判断arraylist为空 一种是 arraylist == null(本身为null) 另一种 是isEmpty() (已经创建,但是没有值)
- 普通数组就可以直接 array == null
-
int compare(T o1,T o2)
Compares its two arguments for order. Returns a negative integer, zero, or a positive integer as the first argument is less than, equal to, or greater than the second.
- 如果求最大最小值的时候,初始化设置不一定是Integer.MAX_VALUE / MIN_VALUE, 很有可能是数组第一个数字,注意题意,容易粗心


- 重做的题
- subarry sum closest
- maximum product subarray
- best time to buy and sell stock iii