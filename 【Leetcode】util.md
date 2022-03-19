# 【Leetcode】util



[toc]



## 打印一维int数组

```c++
void print_1_dim_array_int(int* a, int l_idx, int r_idx) {
	for (int i = l_idx; i <= r_idx; i++) {
		cout << a[i] << " ";
	}
	cout << endl;
}
```

调用示例：

```c++
int arr[10] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
print_1_dim_array_int(arr, 2, 8);
```



## 打印二维int数组

```c++
void print_2_dim_array_int(int* a, int l_row, int l_col, int r_row, int r_col, int col) {
	for (int i = l_row; i <= r_row; i++) {
		for (int j = l_col; j <= r_col; j++) {
			cout << a[i * col + j] << " ";
		}
		cout << endl;
	}
}
```

调用示例：

```c++
int mat[5][6] = {
		{0, 1, 2, 3, 4, 5},
		{6, 7, 8, 9, 10, 11},
		{12, 13, 14, 15, 16, 17},
		{18, 19, 20, 21, 22, 23},
		{24, 25, 26, 27, 28, 29}
};
print_2_dim_array_int((int*)mat, 2, 1, 4, 5, 6);
```



## 打印vector\<int\>

```c++
void print_vector_int(vector<int> v) {
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
}
```



## 打印vector\<vector\<int\>\>

```c++
void print_vector_vector_int(vector<vector<int>> vv) {
	cout << vv.size() << " vectors:" << endl;
	for (vector<vector<int>>::iterator v = vv.begin(); v != vv.end(); v++) {
		for (vector<int>::iterator it = (*v).begin(); it != (*v).end(); it++) {
			cout << *it << " ";
		}
		cout << endl;
	}
}
```

