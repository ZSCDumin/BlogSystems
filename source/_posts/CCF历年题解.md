---
title: CCF历年题解
date: 2018-12-06 15:44:39
tags: CCF c
---

# 出现次数最多的数

```c
#include<iostream>
#include<cstdio>
using namespace std;

int main() {

	int num[10001] = { 0 };
	int n;
	cin >> n;

	for (int i = 0; i < n; i++)
	{
		int t;
		cin >> t;
		num[t] ++;
	}

	int max = 0, index = 0;
	for (int i = 10000; i >= 0; i--)
	{
		if (num[i] >= max){
			max = num[i];
			index = i;
		}
	}
	cout << index << endl;
	return 0;
}
```

# ISBN 号码

```c
#include <iostream>
#include<cstring>
using namespace std;

int main() {

	char s[20];
	int num[20] = { 0 };
	int index = 0;
	cin >> s;
	int len = strlen(s);
	for (int i = 0; i < len; i++){
		if (s[i] == '-'){
			continue;
		}
		else{
			num[index++] = s[i] - '0';
		}
	}
	int sum = 0;
	for (int i = 0; i < index - 1; i++){
		sum += num[i] * (i + 1);
	}
	sum = sum % 11;

	if (sum == 10 && s[len - 1] == 'X' || sum == num[index - 1]){
		cout << "Right" << endl;
	}
	else{
		if (sum == 10)
			s[len - 1] = 'X';
		else
			s[len - 1] = sum + '0';
		cout << s << endl;
	}
	return 0;
}
```

# 跳一跳

```c
#include <iostream>
using namespace std;

int main() {

	int num[31];
	int t,index=0;
	while(1) {
		cin >> t;
		num[index++]=t;
		if(t==0) {
			break;
		}
	}
	int sum=0;
	int count =1;
	for(int i=0; i<index; i++) {
		if(num[i]==1) {
			sum+=1;
			count=1;
		} else if(num[i]==2) {
			sum+=count*2;
			count ++;
		} else {
			break;
		}
	}
	cout<<sum <<endl;
	return 0;
}
```

# 碰撞的小球

```c
#include <iostream>
using namespace std;
int num[105];

int main() {

	int dire[105];
	int n, L, t;

	cin >> n >> L >> t;

	for (int i = 0; i < n; i++) {
		cin >> num[i];
		dire[i] = 1;
	}

	for (int i = 1; i <= t; i++) { //计时器
		for (int j = 0; j < n; j++) {
			//判断方向
			if (num[j] == L && dire[j] == 1 || num[j] == 0 && dire[j] == -1){
				dire[j] *= -1;
			}
			else {
				for (int k = 0; k < n; k++){
					if (num[k] == num[j] && k != j){
						dire[j] *= -1;
						dire[k] *= -1;
					}
				}
			}
			//移动
			num[j] += dire[j];
		}
	}

	for (int j = 0; j < n; j++) {//输出结果
		if (j == n - 1)
			cout << num[j] << endl;
		else
			cout << num[j] << " ";
	}
	return 0;

}
```

# 最小差值

```c
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int num[1005];

int main() {

	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	sort(num, num + n);
	int min = 99999;
	for (int i = 0; i < n - 1; i++){
		if (num[i] == num[i + 1]){
			min = 0;
			break;
		}

		if (min > abs(num[i] - num[i + 1]))
		{
			min = abs(num[i] - num[i + 1]);
		}
	}
	cout << min << endl;
	return 0;

}
```

# 游戏

```c
#include <iostream>
#include <cmath>
#include <queue>
#include <algorithm>
using namespace std;

int num[1005];

int main() {

	int N, K, num = 1;
	queue<int> list;
	cin >> N >> K;

	for (int i = 1; i <= N; i++){
		list.push(i);
	}

	while (list.size() > 1){
		int top = list.front(); //取第一个元素
		list.pop();  //删除第一个元素
		if (num % K != 0 && (num % 10) != K){
			list.push(top);
		}
		num++;
	}

	cout << list.front();
	return 0;
}
```

## 版本二(有点瑕疵,样例: 3 1 通不过)

```c
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int num[1005];

int main() {

	int n, k;
	cin >> n >> k;
	int resNum = n;
	for (int i = 0; i < n; i++){
		num[i] = i + 1;
	}
	int count = 0;
	while (resNum > 1){
		for (int i = 0; i < n; i++){
			if (num[i] != -1){
				count++;
				if (count % k == 0 || count % 10 == k)
				{

					resNum--;
					num[i] = -1;
				}
			}
		}
	}
	for (int i = 0; i < n; i++){
		if (num[i] != -1){
			cout << num[i];
			break;
		}
	}
	return 0;

}
```

## 修订版

```c
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int num[1005];

int main() {

	int n, k;
	cin >> n >> k;
	int resNum = n;
	for (int i = 0; i < n; i++){
		num[i] = i + 1;
	}
	int count = 0;
	for (int i = 0;; i++){
		if (resNum <= 1){
			break;
		}
		if (num[i%n] != -1){
			count++;
			if (count % k == 0 || count % 10 == k)
			{
				resNum--;
				num[i%n] = -1;
			}
		}
	}

	for (int i = 0; i < n; i++){
		if (num[i] != -1){
			cout << num[i];
			break;
		}
	}
	return 0;

}
```

# 分蛋糕

```c
#include <iostream>
#include <cmath>
#include <queue>
#include <algorithm>
using namespace std;
int num[1005];
int main() {
	int n, k;
	int count = 0;
	cin >> n >> k;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int sum = 0;
	for (int i = 0; i < n; i++){
		if (i == n - 1 && sum + num[i] < k){
			count++;
		}
		else
		{
			sum += num[i];
			if (sum >= k){
				count++;
				sum = 0;
			}
		}
	}
	cout << count << endl;
	return 0;
}
```

# 中间数

```c
#include <iostream>
#include <cmath>
#include <queue>
#include <algorithm>
using namespace std;
int num[1005];
int main() {
	int n;
	int flag = 0;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	for (int i = 0; i < n; i++){
		int re1 = 0, re2 = 0;
		for (int j = 0; j < n; j++){
			if (i != j){
				if (num[i] < num[j])
					re1++;
				if (num[i] > num[j])
					re2++;
			}
		}
		if (re1 == re2)
		{
			flag = 1;
			cout << num[i] << endl;
			break;
		}
	}
	if (flag == 0)
		cout << "-1" << endl;
	return 0;
}
```

# 最大波动

```c
#include <iostream>
#include <cmath>
#include <queue>
#include <algorithm>
using namespace std;
int num[1005];
int main() {
	int n;
	int flag = 0;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int max = -1;
	for (int i = 0; i < n-1; i++){
		if (max < abs(num[i] - num[i + 1])){
			max = abs(num[i] - num[i + 1]);
		}
	}
	cout << max << endl;
	return 0;
}
```

# 折点计算

```c
#include <iostream>
#include <cmath>
#include <queue>
#include <algorithm>
using namespace std;
int num[1005];
int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int count = 0;
	int before = num[0] > num[1] ? 0 : 1;
	int after = 0;
	for (int i = 1; i < n - 1; i++){
		if (num[i] > num[i + 1]){
			after = 0;
		}
		else
		{
			after = 1;
		}
		if (before != after){
			count++;
		}
		before = after;
	}
	cout << count << endl;
	return 0;
}
```

# 整数之和

```c
#include <iostream>
#include <cstring>
using namespace std;
int main() {
	char n[30];
	cin >> n;
	int sum = 0;
	for (int i = 0; i < strlen(n); i++){
		sum += n[i] - '0';
	}
	cout << sum << endl;
	return 0;
}
```

# 数列分段

```c
#include <iostream>
#include <cstring>
using namespace std;
int num[1005];

int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int sum = 1;
	for (int i = 0; i < n-1; i++){
		if (num[i] != num[i + 1]){
			sum++;
		}
	}
	cout << sum << endl;
	return 0;
}
```

# 图像旋转

```c
#include <iostream>
#include <cstring>
using namespace std;

int num[1005][1005];

int main() {
	int n, m;
	cin >> n >> m;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			cin >> num[i][j];
		}
	}
	int sum = 1;
	for (int i = 0; i < n - 1; i++){
		if (num[i] != num[i + 1]){
			sum++;
		}
	}
	for (int i = m - 1; i >= 0; i--){
		for (int j = 0; j < n; j++){
			cout << num[j][i] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

# 门禁系统

```c
#include <iostream>
#include <cstring>
using namespace std;

int num[1005];
int res[1005];

int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
		res[i] = 1;
	}
	for (int i = 1; i < n; i++){
		for (int j = 0; j < i; j++){
			if (num[i] == num[j])
				res[i]++;
		}
	}
	for(int i = 0; i < n; i++){
		cout << res[i] << " ";
	}
	return 0;
}
```

# 相邻数对

```c
#include <iostream>
#include <cmath>
using namespace std;

int num[1005];

int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int count = 0;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < n; j++){
			if (i != j)
			{
				if (abs(num[i] - num[j]) == 1)
				{
					count++;
				}
			}
		}
	}
	cout << count / 2 << endl;
	return 0;
}
```

# 相反数

```c
#include <iostream>
#include <cmath>
using namespace std;

int num[1005];

int main() {
	int n;
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int count = 0;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < n; j++){
			if (i != j)
			{
				if (num[i] + num[j] == 0)
				{
					count++;
				}
			}
		}
	}
	cout << count / 2 << endl;
	return 0;
}
```

# 公共钥匙盒

```c
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int num[1005];

struct keys
{
	int keyNum;
	int startTime;
	int endTime;
	int flag;
}keySet[1005];

int flag[1005];

bool compare(keys key1, keys key2){
	return key1.startTime < key2.startTime;
}

int main() {
	int n, k;
	cin >> n >> k;
	int maxLength = 0;
	for (int i = 0; i < k; i++){
		cin >> keySet[i].keyNum >> keySet[i].startTime >> keySet[i].endTime;
		keySet[i].flag = 0;
		flag[i] = i + 1;
		if (maxLength < keySet[i].startTime + keySet[i].endTime){
			maxLength = keySet[i].startTime + keySet[i].endTime;
		}
	}
	sort(keySet, keySet + k, compare);

	/*for (int i = 0; i < k; i++){
		cout << keySet[i].keyNum << " " << keySet[i].startTime << " " << keySet[i].endTime << endl;
		}*/


	for (int i = 1; i <= maxLength; i++){
		for (int j = 1; j <= n; j++){

			if (keySet[j].flag == 0 && keySet[j].startTime >= i && keySet[j].endTime <= i){
				keySet[j].flag = 1;
				flag[keySet[j].keyNum] = -1;
			}

			if (keySet[j].flag == 1 && i > keySet[j].endTime + keySet[j].startTime){
				for (int k = 0; k < n; k++){
					if (flag[k] == -1){
						flag[k] = keySet[j].keyNum;
						keySet[j].flag = 0;
						break;
					}
				}
			}
		}
	}

	for (int i = 0; i < n; i++){
		cout << flag[i] << endl;
	}
	return 0;
}
```

# 除法

```c
#include <iostream>
#include <algorithm>
using namespace std;
long long tree[101024];
int n, m, a[101024];
int lowbit(int x)
{
	return -x&x;
}
void update(int x, int v)
{
	for (int i = x; i <= n; i += lowbit(i))
		tree[i] += v;
}
long long getsum(int x)
{
	long long ans = 0;
	for (int i = x; i > 0; i -= lowbit(i))
		ans += tree[i];
	return ans;
}
int main()
{
	int op, l, r;
	int v;
	cin >> n >> m;
	for (int i = 1; i <= n; ++i)
	{
		cin >> a[i];
		update(i, a[i]);
	}
	for (int i = 0; i < m; i++)
	{
		cin >> op;
		if (op == 1)
		{
			cin >> l >> r >> v;
			if (v == 1)
				continue;
			while (l <= r)
			{
				if (a[l] >= v&&a[l] % v == 0)
				{
					update(l, -(a[l] - a[l] / v));
					a[l] /= v;
				}
				++l;
			}
		}
		else if (op == 2)
		{
			cin >> l >> r;
			cout << getsum(r) - getsum(l - 1) << endl;
		}
	}
	return 0;
}
```

# 字符串匹配

```c
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
string a[105];
string str;
int n, m;
int main()
{
	string::size_type idx;
	getline(cin, str);
	cin >> n;
	cin >> m;
	getchar();
	for (int i = 0; i < m; i++){
		getline(cin, a[i]);
	}
	if (n == 0){
		transform(str.begin(), str.end(), str.begin(), ::tolower);
		for (int i = 0; i < m; i++){
			string t = a[i];
			transform(a[i].begin(), a[i].end(), a[i].begin(), ::tolower);
			idx = a[i].find(str);
			if (idx != string::npos){
				cout << t << endl;
			}
		}
	}
	else
	{
		for (int i = 0; i < m; i++){
			idx = a[i].find(str);
			if (idx != string::npos){
				cout << a[i] << endl;
			}
		}
	}
	return 0;
}
```

# 数字排序

```c
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int n;

struct my{
	int num;
	int count;
}nums[1005];

int compare(my s1, my s2){
	if (s1.count == s2.count)
		return s1.num < s2.num;
	else
		return s1.count > s2.count;
}
int main()
{
	int num[1005] = { 0 };
	cin >> n;

	for (int i = 0; i < n; i++){
		int t;
		cin >> t;
		num[t]++;
	}

	int k = 0;
	for (int i = 0; i < 1001; i++){
		if (num[i] >= 1){
			nums[k].num = i;
			nums[k].count = num[i];
			k++;
		}
	}

	sort(nums, nums + k, compare);

	for (int i = 0; i < k; i++){
		cout << nums[i].num << " " << nums[i].count << endl;
	}

	return 0;
}
```

# Z 形扫描

```c
#include <iostream>
#include <string>
using namespace std;
int n;
int num[505][505];
const int RIGHT = 1; //向右走
const int DOWN = 2; //向下走
const int LEFTDOWN = 3; //向做下走
const int RIGHTUP = 4;  //向右上走

#define max 505

string to_String(int n)
{
	int m = n;
	int i = 0, j = 0;
	char s[max];
	char ss[max];
	while (m > 0)
	{
		s[i++] = m % 10 + '0';
		m /= 10;
	}
	s[i] = '\0';

	i = i - 1;
	while (i >= 0)
	{
		ss[j++] = s[i--];
	}
	ss[j] = '\0';

	return ss;
}
void run(){

	//从第一个位置开始，x为横坐标，y为纵坐标，注意x,y在二维数组中的位置
	int x = 0;
	int y = 0;
	//输出要求有空格隔开
	string result = to_String(num[y][x]) + " ";
	//方向变量的初始值
	int direction = 0;

	//下面就开始出发走咯
	while (!(x == n - 1 && y == n - 1)){//循环直至到达终点（最右下角的位置）
		//先判断下一步往哪个方向走
		if (direction == 0){   //为0说明还没走出第一步，所以接着应该往右边走一步
			direction = RIGHT;
		}
		else if (direction == RIGHT){ //上一次方向向右，下一步应该向左下或者右上
			if (x - 1 >= 0 && y + 1 < n){    //左下可走
				direction = LEFTDOWN;
			}
			else {  //只能走右上了
				direction = RIGHTUP;
			}
		}
		else if (direction == DOWN){   //上一次方向向下，下一步应该向左下或者右上
			if (x - 1 >= 0 && y + 1 < n){    //左下可走
				direction = LEFTDOWN;
			}
			else {  //只能走右上了
				direction = RIGHTUP;
			}
		}
		else if (direction == LEFTDOWN){   //上一次向左下，如果可以，下一步应该继续向左下，否则 向右或者向下走
			if (y + 1 < n && x - 1 >= 0){    //先判断能否继续向左下
				direction = LEFTDOWN;
			}
			else if (y + 1 < n){  //然后判断能否向下走
				direction = DOWN;
			}
			else {      //最后只能向右走了
				direction = RIGHT;
			}
		}
		else if (direction == RIGHTUP){    //上一次向右上，如果可以，下一步应该继续向右上，否则向右或者下走
			if (x + 1 < n && y - 1 >= 0){  //先判断能否继续向右上
				direction = RIGHTUP;
			}
			else if (x + 1 < n){  //然后判断能否向右走
				direction = RIGHT;
			}
			else{            //最后只能向下走了
				direction = DOWN;
			}
		}

		//根据上面确定的方向来走出下一步
		switch (direction){
		case RIGHT: x = x + 1; break;
		case DOWN: y = y + 1; break;
		case LEFTDOWN: x = x - 1; y = y + 1; break;
		case RIGHTUP: x = x + 1; y = y - 1; break;
		}

		//读取当前走到位置的数字.注意x和y的位置
		result += to_String(num[y][x]) + " ";
	}
	cout << result << endl;
}
int main()
{
	cin >> n;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < n; j++){
			cin >> num[i][j];
		}
	}
	run();
	return 0;
}
```

# 日期计算

```c
#include <iostream>
#include <string>
using namespace std;
int n, m;

int month1[12] = { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
int month2[12] = { 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
bool isLeapYear(int year){
	if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0){
		return true;
	}
	else{
		return false;
	}
}
void printMonthAndDay(int flag, int m){
	int days = m;
	int month = 1;
	int day = 0;
	int i = 0;
	if (flag == 0){
		while (days - month1[i] > 0)
		{
			days -= month1[i++];
			month++;
		}
		cout << month << "\n" << days << endl;
	}
	else{
		while (days - month2[i] > 0)
		{
			days -= month2[i++];
			month++;
		}
		cout << month << "\n" << days << endl;
	}
}
int main()
{
	cin >> n >> m;
	int flag = isLeapYear(n);
	printMonthAndDay(flag, m);
	return 0;
}
```

# 火车票

```c
#include <iostream>
using namespace std;
int n;
int num[105];
int seat[20][5];

int main()
{
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> num[i];
	}
	for (int i = 0; i < n; i++){
		int res = num[i];
		int t[100];
		int flag = 0;
		for (int j = 0; j < 20; j++){
			int count = 0;
			int backup[20][5] = { 0 };
			for (int k = 0; k < 5; k++){
				if (seat[j][k] == 0){
					backup[j][k] = 1;
					t[count++] = j * 5 + k + 1;
					for (int l = 1; l < res; l++){
						k++;
						if (seat[j][k] == 1 || k >= 5 || count >= res)
						{
							break;
						}
						else
						{
							t[count++] = j * 5 + k + 1;
							backup[j][k] = 1;
						}
					}
					if (count == res){ //座位够分
						for (int s = 0; s < count; s++){
							cout << t[s] << " ";
						}
						cout << endl;
						for (int x = 0; x < 20; x++){
							for (int y = 0; y < 5; y++){
								if (backup[x][y] == 1)
								{
									seat[x][y] = 1;
								}
							}
						}
						flag = 1;
						break;
					}
					else{ //座位不够分
						break;
					}
				}
			}
			if (flag == 1)
				break;
		}
		if (flag == 0){
			for (int j = 0; j < 20; j++){
				for (int k = 0; k < 5; k++){
					if (seat[j][k] == 0 && res>0){
						seat[j][k] = 1;
						res--;
						cout << j * 5 + k + 1 << " ";
					}
				}
			}
			cout << endl;
		}
	}
	return 0;
}
```

# 俄罗斯方块

```c
#include <iostream>

const int ROW = 15;
const int COL = 10;
const int N = 4;

int board[ROW + 1][COL];
int block[N][N];
struct {
	int row, col;
} coords[N];

using namespace std;

int main()
{
	int row, col;

	// 输入数据
	for (int i = 0; i < ROW; i++)
	for (int j = 0; j < COL; j++)
		cin >> board[i][j];
	for (int i = 0; i < N; i++)
	for (int j = 0; j < N; j++)
		cin >> block[i][j];
	cin >> col;

	// 底边全放1
	for (int j = 0; j < COL; j++)
		board[ROW][j] = 1;

	// 提取小方块坐标
	int k = 0;
	for (int i = N - 1; i >= 0; i--)
	for (int j = 0; j < N; j++)
	if (block[i][j] == 1) {
		coords[k].row = i;
		coords[k].col = j;
		k++;
	}

	// 模拟小方块落下过程（选取参考点原点进行搜索，从当前坐标点开始加上小矩阵元素为1的坐标，
	//判断其位置是否为1 ，位置上为1则停止）
	row = 1;
	col--;
	bool checkflag;
	for (;;) {
		checkflag = false;

		for (int i = 0; i < N; i++)
		if (board[row + coords[i].row][col + coords[i].col] == 1) {
			checkflag = true;
			break;
		}

		if (checkflag)
			break;

		row++;
	}
	row--;

	// 合并小方块到方格
	for (int i = 0; i < N; i++)
		board[row + coords[i].row][col + coords[i].col] = 1;

	// 输出结果
	for (int i = 0; i < ROW; i++) {
		for (int j = 0; j < COL; j++) {
			if (j != 0)
				cout << " ";
			cout << board[i][j];
		}
		cout << endl;
	}
	return 0;
}

```

# 消除类游戏

```c
#include <iostream>
using namespace std;
int num[50][50];
int backup[50][50];
int n, m;
int main()
{
	cin >> n >> m;
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			cin >> num[i][j];
			backup[i][j] = num[i][j];
		}
	}

	// 行扫描
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m - 1; j++){
			int t = num[i][j];
			int count = 1;
			for (int k = j + 1; k < m; k++){
				if (num[i][k] != t)
					break;
				else
					count++;
			}
			if (count >= 3){
				for (int k = j; k < j + count; k++){
					backup[i][k] = 0;
				}
			}
		}
	}

    // 列扫描
	for (int i = 0; i < m; i++){
		for (int j = 0; j < n - 1; j++){
			int t = num[j][i];
			int count = 1;
			for (int k = j + 1; k < n; k++){
				if (num[k][i] != t)
					break;
				else
					count++;
			}
			if (count >= 3){
				for (int k = j; k < j + count; k++){
					backup[k][i] = 0;
				}
			}
		}
	}

	// 输出
	for (int i = 0; i < n; i++){
		for (int j = 0; j < m; j++){
			if (j == m - 1)
				cout << backup[i][j];
			else
				cout << backup[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}

```

# 学生排队

```c
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int n, m;
vector<int> v;
int find(int num){
	for (int i = 0; i < v.size(); i++){
		if (num == v[i])
			return i+1;
	}
	return -1;
}
int main()
{
	cin >> n;
	cin >> m;

	for (int i = 0; i < n; i++){
		v.push_back(i + 1);
	}
	for (int i = 0; i < m; i++){
		int p, q;
		cin >> p >> q;
		int pos = find(p);
		//cout << pos << endl;
		if (q >= 0){
			//cout << *v.begin() << endl;
			v.insert(v.begin() + pos + q, p);
			v.erase(v.begin() + pos - 1);
		}
		else{
			//cout << *v.begin() << endl;
			v.insert(v.begin() + pos - 1 + q, p);
			v.erase(v.begin() + pos);
		}
	}
	for (int i = 0; i < v.size(); i++){
		cout << v[i] << " ";
	}
}
```

# 地铁修建

```c
# include <iostream>
# include <queue>
# include <functional>
using namespace std;

typedef pair<int, int> pii;
const int maxn = 100000 + 100;
const int INF = INT_MAX;
struct node
{
	int from, to, dist;
	node(int from, int to, int dist) :from(from), to(to), dist(dist){}
};
int n, m;
vector<node> edges;
vector<int> g[maxn];
bool visited[maxn];
int d[maxn];
void AddEdge(int from, int to, int dist)
{
	edges.push_back(node(from, to, dist));
	g[from].push_back(edges.size() - 1);
}
void dij(int start)
{
	priority_queue<pii, vector<pii>, greater<pii> >q;//d和from
	for (int i = 0; i<n; i++) d[i] = INF;
	d[start] = 0;
	memset(visited, 0, sizeof(visited));
	q.push(make_pair(0, start));
	while (!q.empty()){
		pii x = q.top(); q.pop();
		int u = x.second;
		if (visited[u]) continue;
		visited[u] = true;
		for (int i = 0; i<g[u].size(); i++){
			node &e = edges[g[u][i]];
			//if (d[e.to]>max(d[u], e.dist)){//改变松弛策略
			//	d[e.to] = max(d[u], e.dist);
			//	q.push(make_pair(d[e.to], e.to));
			//}
			if (d[e.to]> d[u] + e.dist){//改变松弛策略
				d[e.to] = d[u] + e.dist;
				q.push(make_pair(d[e.to], e.to));
			}
		}
	}
}
int main()
{
	cin >> n >> m;
	for (int i = 0; i<m; i++){
		int a, b, c;
		cin >> a >> b >> c;
		AddEdge(a - 1, b - 1, c);// 只写一个代表：有向图
		//AddEdge(b - 1, a - 1, c); //两个同时写代表：无向图
	}

	dij(0);
	cout << d[n - 1] << endl;
	return 0;
}
```

# 棋局评估

```c
#include <iostream>
#include <cstring>
#include <map>
using namespace std;
int a[9];
map<int, int> mymap;

int isover(){
	for (int i = 0; i < 3; i++){    //检测列，仔细计算下，容易出错
		if (a[i] == a[i + 3] && a[i] == a[i + 6] && a[i])
			return a[i];
	}
	for (int i = 0; i < 9; i += 3){//检测行
		if (a[i] == a[i + 1] && a[i] == a[i + 2] && a[i])
			return a[i];
	}
	if (a[0] == a[4] && a[0] == a[8] && a[0])//检测对角
		return a[0];
	if (a[2] == a[4] && a[2] == a[6] && a[2])
		return a[2];
	return 0;
}

int dp(){
	int aa = 0; //状态
	for (int i = 0; i < 9; i++){
		aa = aa * 10 + a[i];
	}
	if (mymap.find(aa) != mymap.end()){ //记忆化搜索，若当前状态出现过，则不再重新计算。
		return mymap[aa];
	}

	int ct = 0;
	for (int i = 0; i < 9; i++) //找空余的0
	if (a[i])
		ct++;
	int rt = isover();
	if (rt == 1) //Alice赢
		return 10 - ct;
	if (rt == 2) // Bob赢
		return -(10 - ct);
	if (ct == 9 && rt == 0) //下满了，并且未分出胜负，则平局
		return 0;
	int an = 0;
	if (ct % 2 == 0){ //轮到Alice
		an = -100;
		for (int i = 0; i < 9; i++){
			if (a[i] == 0){    //遍历所有空格
				a[i] = 1;

				int s = dp();
				if (an < s){  //找到得分最高的
					an = s;
				}
				a[i] = 0;
			}
		}
	}
	else{   //轮到Bob
		an = 100;
		for (int i = 0; i < 9; i++){
			if (a[i] == 0){
				a[i] = 2;

				int s = dp();
				if (an > s){//找到得分最低的
					an = s;
				}
				a[i] = 0;
			}
		}
	}
	return mymap[aa] = an;
}

int main(){
	int t;
	cin >> t;
	while (t--){
		mymap.erase(mymap.begin(), mymap.end());
		for (int i = 0; i < 9; i++)   {
			cin >> a[i];
		}
		cout << dp() << endl;
	}

	return 0;
}
```

# 最大的矩形

```c
#include<iostream>
#include <vector>
#include <algorithm>
using namespace std;
int n;
int num[1005];

int find_min(int i, int j){
	int min = 99999999;
	for (int k = i; k <= j; k++){
		if (num[k] < min){
			min = num[k];
		}
	}
	return min;
}
int main(){
	cin >> n;
	for (int i = 0; i < n; i++){
		cin >> num[i];
	}
	int max = -99999;
	for (int i = 0; i < n-1; i++){
		for (int j = i+1; j < n; j++){
			int res = find_min(i, j) * (j-i+1);
			if (res > max){
				max = res;
			}

		}
	}
	cout << max << endl;
	return 0;
}
```

# 有趣的数

```c
#include <iostream>

using namespace std;

/* 状态分析： states[i][0]表示第i位状态为0的情况
0－－用了2，剩0，1，3
1－－用了0，2，剩1，3
2－－用了2，3，剩0，1
3－－用了0，1，2，剩3
4－－用了0，2，3，剩1
5－－全部用了
*/

long long states[1005][6];

int main(){

	long mod = 1000000007;
	int n;
	cin >> n;

	for (int i = 0; i<6; i++)
		states[0][i] = 0;

	for (int i = 1; i <= n; i++)
	{
		int j = i - 1;

		//只能以2开头，所以只存在一种情况
		states[i][0] = 1;

		//1、可以由第i-1步状态为0到达状态第i步的状态1
		//2、可以由第i-1步状态为1到达状态第i步的状态1，此时第i位只能填2或0。
		states[i][1] = (states[j][0] + states[j][1] * 2) % mod;

		//1、可以由第i-1步状态为0到达状态第i步的状态2
		//2、可以由第i-1步状态为2到达状态第i步的状态2，此时第i位只能填3。
		states[i][2] = (states[j][0] + states[j][2]) % mod;

		//1、可以由第i-1步状态为1到达状态第i步的状态3。
		//2、可以由第i-1步状态为3到达状态第i步的状态3，此时第i位只能填3或1。
		states[i][3] = (states[j][1] + states[j][3] * 2) % mod;

		//1、可以由第i-1步状态为1或者2到达状态第i步的状态4。
		//2、可以由第i-1步状态为4到达状态第i步的状态4，此时第i位只能填3或1。
		states[i][4] = (states[j][1] + states[j][2] + states[j][4] * 2) % mod;

		//1、第i-1步只剩一个数字到达第i步的状态,此时第i位只能填1或3。
		//2、第i-1步不剩任何数字到达第i步的状态，此时此时第i位只能填3或1。
		states[i][5] = (states[j][3] + states[j][4] + states[j][5] * 2) % mod;
	}
	cout << states[n][5] << endl;
	return 0;
}
```
