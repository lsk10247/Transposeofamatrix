#include <stdlib.h>
#include <stdio.h>
#include <iostream>
#include <iomanip>
#include<string>
using namespace std;
//三元组节点定义
typedef int elemtype;
typedef struct
{
	int row;  //行下标
	int col;  //列下标
	elemtype value;  //元素值
}Triple;


//三元组顺序表定义
#define MAX_SIZE 100   
typedef struct
{
	int rn;  //行数
	int cn;  //列数
	int tn;  //非0元素个数
	Triple data[MAX_SIZE];
}TMatrix;

void sortMatrix(TMatrix& matrix) {
	for (int start = 0;start < matrix.tn - 1;start++) {
		int min = matrix.data[start].row;
		int minIndex = start;
		for (int i = start;i < matrix.tn;i++) {
			if (matrix.data[i].row < min) {
				min = matrix.data[i].row;
				minIndex = i;
			}
		}
		Triple temp;
		temp = matrix.data[start];
		matrix.data[start] = matrix.data[minIndex];
		matrix.data[minIndex] = temp;
	}
}

void TransMatrix(TMatrix a, TMatrix& b)
{
	int p, q = 0, col;
	b.rn = a.cn;      
	b.cn = a.rn;      
	b.tn = a.tn;//ab矩阵行列号交换

	//将b中的元素全部变为0
	for (int i = 0;i < b.tn;i++) {
		b.data[i].value = 0;
	}

	if (b.tn == 0) printf("The Matrix a = 0!\n");
	else    
	{
		for (int i = 0;i < b.tn;i++) {
			b.data[i].row = a.data[i].col;
			b.data[i].col = a.data[i].row;
			b.data[i].value = a.data[i].value;
		}
		sortMatrix(b);
	}
}



void QuickTransMatrix(TMatrix a, TMatrix& b) {
	b.rn = a.cn;
	b.cn = a.rn;
	b.tn = a.tn;//ab矩阵行列号交换

	int p = 0, q = 0;

	int num[MAX_SIZE];
	int cpot[MAX_SIZE];
	for (int i = 0;i < MAX_SIZE;i++) {
		num[i] = 0;
		cpot[i] = 0;
	}
	cpot[1] = 1;

	for (int i = 0;i < a.tn;i++) {
		if (a.data[i].value != 0) {
			num[a.data[i].col]++;
		}
	}
	for (int i = 2;i < MAX_SIZE;i++) {
		cpot[i] = cpot[i - 1] + num[i - 1];
	}
	for (int i = 0;i < a.tn;i++) {
		if (a.data[i].value != 0) {
			b.data[cpot[a.data[i].col+1] - 1 - num[a.data[i].col]].value = a.data[i].value;
			b.data[cpot[a.data[i].col+1] - 1 - num[a.data[i].col]].row = a.data[i].col;
			b.data[cpot[a.data[i].col+1] - 1 - num[a.data[i].col]].col = a.data[i].row;
			num[a.data[i].col]--;
		}
	}
}

int main()
{
	restart:
	cout << "1.原题\n" << "2.附加题" << endl;
	string judge;
	cin >> judge;
	if (judge == "1") {
		cout << "已选择原题" << endl;
	}
	else if (judge == "2") {
		cout << "已选择附加题" << endl;
	}
	else {
		cout << "请输入1或2！"<<endl;
		goto restart;
	}
	TMatrix a, b;      
	a.tn = 0; 
	b.tn = 0;
	cout << "输入矩阵a行数：\n";      
	cin >> a.rn;
	cout << "输入矩阵a列数：\n";      
	cin >> a.cn;
	cout << "按行优先次序输入矩阵a元素：\n";
	for (int i = 0; i < a.rn; i++)//i代表行
	{
		for (int j = 0; j < a.cn; j++)//j代表列
		{
			int e;
			cin >> e;
			if (e != 0) {
				a.data[a.tn].value = e;
				a.data[a.tn].row = i+1;
				a.data[a.tn].col = j+1;
				a.tn++;
			}
		}
		cout << "\n";
	}

	//进行矩阵的转置
	if (judge == "1") {
		TransMatrix(a, b);
	}
	else if (judge == "2") {
		QuickTransMatrix(a, b);
	}
	//清空缓冲区
	while (getchar()!='\n');
	cout << "是否输出转置后的矩阵？YES/NO" << endl;
	cin >> judge;
	if (judge == "YES")
	{
		cout << "输出转置矩阵b:\n";
		cout << "行" << setw(4) << "列" <<setw(4)<< "值" << endl;
		for (int i = 0;i < b.tn;i++) {
			cout << b.data[i].row;
			cout << setw(4);
			cout << b.data[i].col;
			cout << setw(4);
			cout << b.data[i].value << endl;
		}
	}
	else
		cout << "矩阵已转置完成并进入三元顺序表";
}

