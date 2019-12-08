# So-many-queens
This is a method to solve the eight queens puzzle or even more queens. 

#include <cmath>
#include <cstdlib>
#include <iomanip>
#include <ctime>
#include <iostream>
#include <Windows.h>
unsigned long long beginTick;
using namespace std;
//开始 begintick
void Begin()
{
	cout << "皇后问题开始计算...." << endl;
    beginTick = ::GetTickCount64();
}
//结束 endtickang
void End() 
{
	unsigned long long endTick = ::GetTickCount64();
	cout << "计算所需时间" << (endTick - beginTick) / 1000.0 << "s" << endl;
}
//棋盘的初始化
void Start(int a[], int N)
{
	for (int i = 0; i < N; ++i)
		a[i] = i;
}	
//对棋盘进行交换操作
void Swap(int a[], int N, int errorid)
{
	int k;
	do{
	k = rand() % N;
	}while (k == errorid);
	int temp = a[k];
	a[k] = a[errorid];
	a[errorid] = temp;
}
//检查函数
int Check(int a[],int N) 
{
	int temp = -1;
	for (int i = 0; i < N; ++i)
	{
		for (int j =i+1; j < N; ++j) 
		{
			if (fabs(a[i] - a[j]) == fabs(i - j)) 
			{
				temp = i;
				break;
			}
		}
	}
	return temp;
}
//输出皇后所在位置
void Print(int a[], int N)
{
	for (int i = 0; i < N; ++i)
	{
		for (int j = 0; j < N; ++j)
		{
			if (a[i] == j) cout<<"■";
			else cout<<"□";
		}
		cout << endl;
	}
	cout << endl;
}

//皇后问题
int main()
{
	int work = 0;
	srand(time(0));
	int errorid=0;
	int N;
	int ;
	cout << "请输入皇后个数" << endl;
	cin >> N;
	int* chess = new int[N];
	Start(chess, N);
	Begin();
	for (;;) 
	{   
		Swap(chess, N, errorid);
		errorid = Check(chess, N);
		++work;
		if (errorid == -1) break;
	}
	End();
	Print(chess, N);
	cout << endl;
	cout << "工作量为" << work;
}
