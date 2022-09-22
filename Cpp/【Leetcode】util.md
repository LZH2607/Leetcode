# 【Leetcode】util



[toc]



## 打印一维数组

```c++
template<class T>
void print_1_dim_array(T* a, int l_idx, int r_idx) {
	for (int i = l_idx; i <= r_idx; i++) {
		cout << a[i] << "  ";
	}
	cout << endl;
}
```

调用示例：

```c++
int a[10] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
double b[10] = { 0.1, 1.1, 2.1, 3.1, 4.1, 5.1, 6.1, 7.1, 8.1, 9.1 };
print_1_dim_array(a, 2, 8);
print_1_dim_array(b, 5, 9);
```



## 打印二维数组（一级指针）

```c++
template<class T>
void print_2_dim_array_by_pointer(T* a, int row1, int col1, int row2, int col2, int col) {
	for (int i = row1; i <= row2; i++) {
		for (int j = col1; j <= col2; j++) {
			cout << a[i * col + j] << "  ";
		}
		cout << endl;
	}
}
```

调用示例：

```c++
int a[5][6] = {
		{0, 1, 2, 3, 4, 5},
		{6, 7, 8, 9, 10, 11},
		{12, 13, 14, 15, 16, 17},
		{18, 19, 20, 21, 22, 23},
		{24, 25, 26, 27, 28, 29}
};
double b[5][6] = {
	{0.1, 1.1, 2.1, 3.1, 4.1, 5.1},
	{6.1, 7.1, 8.1, 9.1, 10.1, 11.1},
	{12.1, 13.1, 14.1, 15.1, 16.1, 17.1},
	{18.1, 19.1, 20.1, 21.1, 22.1, 23.1},
	{24.1, 25.1, 26.1, 27.1, 28.1, 29.1}
};
print_2_dim_array_by_pointer((int*)a, 2, 1, 4, 5, 6);
print_2_dim_array_by_pointer((double*)b, 2, 1, 3, 4, 6);
```



## 打印二维数组（二级指针）

```c++
template<class T>
void print_2_dim_array_by_double_pointer(T** a, int row1, int col1, int row2, int col2) {
	for (int i = row1; i <= row2; i++) {
		for (int j = col1; j <= col2; j++) {
			cout << a[i][j] << "  ";
		}
		cout << endl;
	}
}
```

调用示例：

```c++
int row = 4;
int col = 5;
int** a = (int**)malloc(sizeof(int*) * row);
for (int i = 0; i < row; i++) {
	a[i] = (int*)malloc(sizeof(int) * col);
}
for (int i = 0; i < row; i++) {
	for (int j = 0; j < col; j++) {
		a[i][j] = 10 * i + j;
	}
}
print_2_dim_array_by_double_pointer(a, 1, 1, 3, 3);
```



## 打印vector\<T\>

```c++
template<class T>
void print_vector(vector<T>& v) {
	for (typename vector<T>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << "  ";
	}
	cout << endl;
}
```

调用示例：

```c++
vector<int> a = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
vector<double> b = { 0.1, 1.1, 2.1, 3.1, 4.1, 5.1, 6.1, 7.1, 8.1, 9.1 };
print_vector(a);
print_vector(b);
```



## 打印vector\<vector\<T\>\>

```c++
template<class T>
void print_vector_vector(vector<vector<T>>& vv) {
	cout << vv.size() << " vectors:" << endl;
	for (typename vector<vector<T>>::iterator v = vv.begin(); v != vv.end(); v++) {
		for (typename vector<T>::iterator it = (*v).begin(); it != (*v).end(); it++) {
			cout << *it << "  ";
		}
		cout << endl;
	}
}
```

调用示例：

```c++
vector<vector<int>> a = {
		{0, 1, 2, 3, 4, 5, 6, 7, 8, 9},
		{10, 11, 12, 13, 14, 15, 16, 17, 18, 19},
		{20, 21, 22, 23, 24, 25, 26, 27, 28, 29}
};
print_vector_vector(a);
```



## 打印map\<key, val\>

```c++
template<class key, class val>
void print_map(map<key, val>& m) {
	cout << "key  value" << endl;
	cout << "----------" << endl;
	for (typename map<key, val>::iterator it = m.begin(); it != m.end(); it++) {
		cout << (*it).first << "  " << (*it).second << endl;
	}
}
```

调用示例：

```c++
map<string, int> m;;
m["apple"] = 1;
m["banana"] = 2;
m["cat"] = 3;
print_map(m);
```



## 打印unordered_map\<key, val\>

```c++
template<class key, class val>
void print_unordered_map(unordered_map<key, val>& m) {
	cout << "key  value" << endl;
	cout << "----------" << endl;
	for (typename unordered_map<key, val>::iterator it = m.begin(); it != m.end(); it++) {
		cout << (*it).first << "  " << (*it).second << endl;
	}
}
```

调用示例：

```c++
unordered_map<string, int> m;;
m["apple"] = 1;
m["banana"] = 2;
m["cat"] = 3;
print_unordered_map(m);
```

