---
title : # Selection Sort
date : 2023-09-07 00:00:00 +/-TTTT
categories : [Data Structure, Selection Sort]
tags : [selection_sort] #소문자만 가능
---
```cpp
#include <iostream>
#include <cassert>
#include <fstream>

using namespace std;

struct Element
{
	int key;
	char value;
};

bool CheckSorted(int* arr, int size)
{
	// TODO: 정렬 확인 함수 구현
	for(int e = 0; e < size-1; e++)
	{
	    if(arr[e] > arr[e+1]) return false;
	}

	return true;
}

void Print(int* arr, int size)
{
	for (int i = 0; i < size; i++)
		cout << arr[i] << " ";
	cout << endl;
}

void Print(Element* arr, int size)
{
	for (int i = 0; i < size; i++)
		cout << arr[i].key << " ";
	cout << endl;

	for (int i = 0; i < size; i++)
		cout << arr[i].value << " ";
	cout << endl;
}

int main()
{
	// 3개 정렬
	{
		for (int k = 0; k < 3; k++)
			for (int j = 0; j < 3; j++)
				for (int i = 0; i < 3; i++) {

					int arr[3] = { i, j, k };
					int size = sizeof(arr) / sizeof(arr[0]);

					for (int e = 0; e < size; e++) {
						cout << arr[e] << " " << flush;
					}

					cout << " -> " << flush;

					//TODO: 정렬 해보기
					for (int i = 0; i < size; i++)
					{
					    for(int j = i+1; j < size; j++)
					    {
					        if(arr[i] > arr[j])
    					    {
    					        int tmp = arr[i];
    					        arr[i] = arr[j];
    					        arr[j] = tmp;
    					    }
					    }
					}

					for (int e = 0; e < size; e++) {
						cout << arr[e] << " " << flush;
					}

					cout << boolalpha;
					cout << CheckSorted(arr, size); // 정렬 되었나 확인
					cout << endl;
				}
	}

	//return 0; // <- 실습용 임시

	// 5개라면? 더 많다면?
	{
		// 8 4 2 8 3
		// TODO: ???

		// 8 3 2 5 1 1 2 5 8 9
		// TODO: ???

		// 100개라면?
	}

	// 가장 작은 수 찾기
	{
		int arr[] = { 8, 3, 2, 5, 1, 1, 2, 5, 8, 9 }; // 임의의 숫자들, 변경 가능
		int size = sizeof(arr) / sizeof(arr[0]);

		assert(size > 0); // size가 1이상이라고 가정

		// TODO:
		int min_number = arr[0];
		for(int e = 0; e < size; e++)
		{
		    if(min_number > arr[e]) min_number = arr[e];
		    //min_number = arr[e] < min_number ? arr[i] : min_number;
		    //min_number = std::min(arr[i], min_number);
		}

		cout << "Minimum number is " << min_number << endl;
	}
	//return 0;

	// 가장 작은 수의 인덱스 찾기
	{
		int arr[] = { 8, 3, 2, 5, 1, 1, 2, 5, 8, 9 };
		int size = sizeof(arr) / sizeof(arr[0]);

		assert(size > 0); // size가 1이상이라고 가정

		// TODO:
		int min_index = 0;
		for(int e = 1; e < size; e++)
		{
		    if(arr[e] < arr[min_index]) min_index = e;
		}

		cout << "The index of min is " << min_index << endl;
	    cout << "Minimum number is " << arr[min_index] << endl;
	}
	//return 0;

	// Selection Sort
	// 힌트: swap()
	
	//8 3 2 5
	//2 3 8 5
	//2 3 8 5
	//2 3 5 8
	{
		int arr[] = { 8, 3, 2, 5, 1, 1, 2, 5, 8, 9 };
		int size = sizeof(arr) / sizeof(arr[0]);

		int min_index;
		for (int i = 0; i < size - 1; i++)
		{

			// TODO:
			//1. 가장 작은 값의 index 찾기
			int min_index = i;
			for(int e = i+1; e < size; e++)
			{
			    if(arr[e] < arr[min_index]) min_index = e;
			}
			//2. 가장 작은 값의 index와 i와 swap
			swap(arr[min_index], arr[i]);

			Print(arr, size);

			cout << boolalpha;
			cout << CheckSorted(arr, size);
			cout << endl;
		}
	}
	//return 0;
	// 비교 횟수 세보기, 더 효율적인 방법은 없을까?
	// https://en.wikipedia.org/wiki/Sorting_algorithm
	{
		ofstream ofile("log.txt");
		for (int size = 1; size < 1000; size++)
		{
			int count = 0;
			int* arr = new int[size];
			for (int s = 0; s < size; s++) {
				arr[s] = size - s;
			}

			//TODO: count ++;
    		int min_index;
    		for (int i = 0; i < size - 1; i++)
    		{
    
    			// TODO:
    			//1. 가장 작은 값의 index 찾기
    			int min_index = i;
    			for(int e = i+1; e < size; e++)
    			{
    			    count++;
    			    if(arr[e] < arr[min_index]) min_index = e;
    			}
    			//2. 가장 작은 값의 index와 i와 swap
    			swap(arr[min_index], arr[i]);

    		}

			//cout << size << ", " << count << endl;
			ofile << size << ", " << count << endl;
			// Print(arr, size);

			delete[] arr;
		}

		ofile.close();
	}
	//return 0;

	// [2, 2, 1]
	// [1, 2, 2] // 첫 2가 마지막으로 이동

	// 안정성 확인(unstable)
	// key 값이 같은데 value 순서가 바뀌면 unstable
	// key 값이 같은데 value 순서가 그대로이면 stable
	{
		Element arr[] = { {2, 'a'}, {2, 'b'}, {1, 'c'} };
		int size = sizeof(arr) / sizeof(arr[0]);

		Print(arr, size); // arr이 Element의 배열

		// TODO:
    	int min_index;
    	for (int i = 0; i < size - 1; i++)
		{
    		int min_index = i;
			for(int e = i+1; e < size; e++)
    		{
    		    if(arr[e].key < arr[min_index].key) min_index = e;
    		}
    		swap(arr[min_index], arr[i]);
		}		
		

		Print(arr, size); // arr이 Element의 배열
	}
	return 0;
}
```

💡선택정렬 구현 전략

1. 가장 작은거 고르고 앞으로 빼기
2. 나머지 중 가장 작은거 고르고 빼기 반복
3. 메모리 문제때문에 swap 사용하기
4. 마지막 하나는 볼 필요 없다 가장 크기 때문

stable :  key 값이 같을때 value 순서가 유지 됨.

unstable : key 값이 같을때 value 순서가 유지 되지 못함.