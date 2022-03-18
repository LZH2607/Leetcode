# 【Leetcode】util



[toc]



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

