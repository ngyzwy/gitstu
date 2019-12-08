### 基姆拉尔森计算公式计算星期几

```c++
char week[7][20] = {"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};

if (m == 1 || m == 2) {
	m += 12;
	y--;
}

int w = (d + 2 * m + 3 * (m + 1) / 5 + y + y / 4 - y / 100 + y / 400 + 1) % 7;

cout << week[w] << endl;
```

