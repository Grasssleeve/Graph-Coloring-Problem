# Graph-Coloring-Problem
Using 3 ways to solve the problem: Tabu Search, Hybrid Evolutionary Algorithms and HEA in Duet.

## Description

*Tabu08.cpp* uses algorithm from [Using tabu search techniques for graph coloring](https://link.springer.com/article/10.1007/BF02239976).

*HEA02.cpp* uses algorithm from [Hybrid Evolutionary Algorithms for Graph Coloring](https://link.springer.com/article/10.1023/A:1009823419804).

*HEAD01.cpp* uses algorithm from [Variations on memetic algorithms for graph coloring problems](https://link.springer.com/article/10.1007/s10732-017-9354-9).

*DSJC500.5.col* is the test instance.

The last one is published in Feb, 2018 and is the fastest one among these 3 ways. And its best solution is K=47.

Tabu search is the foundation of other 2 ways.

Thanks for [chenfengkg](https://github.com/chenfengkg) 's article [禁忌搜索算法解决图着色问题](https://blog.csdn.net/hujinglovekmg/article/details/79203792). Tabu08.cpp borrowed his ideas and I made some changes in judgment condition to make it more concise.

The main difference from his code is the way to select move, shown as following.

```c++
if (tmp_delt <= delt && ( iter> h_tabu[j]|| (tmp_delt + f)<best_f)) { // 1&&(2||3)
    if (tmp_delt < delt) {//当前解小于本次迭代最优解,则重新开始保存解
    equ_count = 0;
    delt = tmp_delt;
    }
    equ_delt[equ_count][0] = i;
    equ_delt[equ_count][1] = j;
    equ_count++;
}
```

```c++
 int tmp = rand() % equ_count;//有多个解时，随机选择
    sel_vertex = equ_delt[tmp][0];
    sel_color = equ_delt[tmp][1];
```

## Result

Using *DSJC500.5.col* to test.

### Tabu

K=49

|            | 迭代次数     | 时间(ms)     | 迭代频率(次/s) |
| ---------- | ------------ | ------------ | -------------- |
| 1          | 6637998      | 20931        | 317137         |
| 2          | 23955577     | 75391        | 317751         |
| 3          | 38922336     | 123361       | 315516         |
| 4          | 96602832     | 302124       | 319746         |
| 5          | 12942501     | 40556        | 319127         |
| 6          | 2570572      | 8239         | 312000         |
| 7          | 139941246    | 439614       | 318328         |
| 8          | 218616457    | 690711       | 316509         |
| 9          | 52939800     | 168495       | 314192         |
| 10         | 7037286      | 21899        | 321352         |
| 11         | 9168899      | 28408        | 322758         |
| 12         | 13672252     | 41232        | 331593         |
| **平均值** | **51917313** | **163413.4** | **318834**     |

### HEA

K=49, L=4000

| CrossIter | time  | 平均迭代频率（次/s) |
| --------- | ----- | ------------------- |
| 450       | 6696  | 67.20430108         |
| 495       | 7977  | 62.05340354         |
| 595       | 8817  | 67.48327095         |
| 306       | 5263  | 58.14174425         |
| 710       | 10853 | 65.41969962         |
| 963       | 13594 | 70.8400765          |
| 338       | 4866  | 69.46157008         |
| 261       | 4857  | 53.73687461         |
| 391       | 6020  | 64.95016611         |
| 644       | 8695  | 74.06555492         |

K=48,L=10000

| CrossIter | time  |
| --------- | ----- |
| 1767      | 59003 |
| fail      |       |
| 887       | 32752 |
| fail      |       |
| 1736      | 62200 |
| 1212      | 42157 |

平均迭代频率（次/s) 67.20430108

### HEAD

K=48,L=10000

| No.    | Cross  | Time(ms) | 频率（次/s) |
| ------ | ------ | -------- | ----------- |
| 1      | 2229   | 128406   | 17.36       |
| 2      | 1068   | 65191    | 16.38       |
| 3      | 789    | 51019    | 15.46       |
| 4      | 2958   | 172251   | 17.17       |
| 5      | 836    | 52173    | 16.02       |
| 6      | 686    | 39936    | 17.18       |
| 7      | 261    | 16835    | 15.50       |
| 8      | 625    | 36765    | 17.00       |
| 9      | 567    | 40804    | 13.90       |
| 10     | 1286   | 74541    | 17.25       |
| 11     | 820    | 52239    | 15.70       |
| 12     | 2390   | 134129   | 17.82       |
| 13     | 281    | 17966    | 15.64       |
| 14     | 366    | 22365    | 16.36       |
| 15     | 322    | 22315    | 14.43       |
| 16     | 793    | 53158    | 14.92       |
| 17     | 471    | 28723    | 16.40       |
| 18     | 1884   | 110997   | 16.97       |
| 19     | 2699   | 150712   | 17.91       |
| 20     | 375    | 25023    | 14.99       |
| 平均值 | 1085.3 | 64777.4  | 16.22       |

