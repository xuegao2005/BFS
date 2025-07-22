![image-20250603114624876](https://github.com/xuegao2005/BFS/blob/main/image-20250603114624876.png)

手写队列

```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>

using namespace std;

typedef pair<int, int> PII; // 定义一个整型对

const int N = 110;

int n, m;
int g[N][N]; // 地图，g[i][j] = 0 表示空地，g[i][j] = 1 表示障碍物
int d[N][N]; // 距离数组，d[i][j] 表示从起点到 (i, j) 的最短距离
PII q[N * N]; // 队列，存储坐标对

int bfs() {
    int hh = 0, tt = 0; // 队列头和队列尾
    q[0] ={0, 0}; // 起点坐标

    memset(d, -1, sizeof d); // 初始化距离数组为 -1
    d[0][0] = 0; // 起点距离为 0

    int dx[4] = {0, 0, 1, -1}, dy[4] = {1, -1, 0, 0}; // 四个方向的移动 

    while (hh <= tt) 
    {
        auto t = q[hh++]; // 取出队列头元素

        for (int i = 0; i < 4; i++)
        {
            // 计算新坐标
            // 如果新坐标在边界内且未被访问过且不是障碍物，则更新距离并加入队列
            int x = t.first + dx[i], y = t.second + dy[i];
            if (x >= 0 && x < n && y >= 0 && y < m && g[x][y] == 0 && d[x][y] == -1) 
            {
                d[x][y] = d[t.first][t.second] + 1; // 更新距离
                q[++tt] = {x, y}; // 将新坐标加入队列
            }
        }
    }
    return d[n - 1][m - 1];
}

int main() {
    cin >> n >> m;

    // 输入地图
    for (int i = 0; i <n; i++)
        for (int j = 0; j < m; j++)
            cin >> g[i][j];

    cout << bfs() << endl;
    return 0;
}
```

用stl的queue

```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <queue>

using namespace std;

typedef pair<int, int> PII; // 定义一个整型对

const int N = 110;

int n, m;
int g[N][N]; // 地图，g[i][j] = 0 表示空地，g[i][j] = 1 表示障碍物
int d[N][N]; // 距离数组，d[i][j] 表示从起点到 (i, j) 的最短距离

int bfs() {
    queue<PII> q; // 队列用于 BFS
    q.push({0, 0}); // 起点入队

    memset(d, -1, sizeof d); // 初始化距离数组为 -1
    d[0][0] = 0; // 起点距离为 0

    int dx[4] = {0, 0, 1, -1}, dy[4] = {1, -1, 0, 0}; // 四个方向的移动 右, 左, 下, 上

    while (!q.empty()) 
    {
        PII t = q.front(); // 取出队首元素
        q.pop(); // 弹出队首元素

        // 枚举四个方向
        for (int i = 0; i < 4; i++)
        {
            // 计算新坐标，如果新坐标在边界内且未被访问过且不是障碍物，则更新距离并加入队列
            int x = t.first + dx[i], y = t.second + dy[i];
            if (x >= 0 && x < n && y >= 0 && y < m && g[x][y] == 0 && d[x][y] == -1) 
            {
                d[x][y] = d[t.first][t.second] + 1; // 更新距离
                q.push({x, y}); // 新坐标入队
            }
        }
    }
    return d[n - 1][m - 1];
}

int main() {
    cin >> n >> m;

    // 输入地图
    for (int i = 0; i <n; i++)
        for (int j = 0; j < m; j++)
            cin >> g[i][j];

    cout << bfs() << endl;
    return 0;
}
```

