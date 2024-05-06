---
title:  "���� 1927-�ּ���"
excerpt: "md ���Ͽ� ��ũ�ٿ� �������� �ۼ��Ͽ� Github ���� ����ҿ� ���ε� �غ���. �����ʹ� Visual Studio code ���! ���� �������� Ȯ�ε� �غ���. "

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git, baekjoon]

toc: true
toc_sticky: true
 
date: 2024-04-25
last_modified_at: 2024-04-25
---

2024-4-35�� ���� 1927-�ּ��� ������ Ǯ����

https://www.acmicpc.net/problem/1927

![image](https://github.com/softkleenex/softkleenex.github.io/assets/92619941/e71e63ee-850f-45a9-a36f-99a5e5c58ea5)


ü���� �ҽ��ڵ�� ������ ����.

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#define swap(a, b) do{int temp = a; a = b; b = temp;}while(0)

int heap[100000];
int size = 0;



int parent(int index)
{ 
    return (index -1) /2;
}

int leftChild(int index)
{ 
    return (index)*2 +1;
}

int rightChild(int index)
{ 
    return (index)*2 + 2;
}


void insert(int value)
{
    if (size == 9999)
    {}    //���� �� á��
    
    int index = size;
    heap[size] = value;
    size ++;
    
    while ((index != 0) && (heap[parent(index)] > heap[index]))
    {
        swap(heap[index], heap[parent(index)]);
        index = parent(index);
    }
}




void minHeapify(int index)
{
    int left = leftChild(index);
    int right = rightChild(index);
    int smallest = index;

    if (left < size && heap[left] < heap[smallest])
        smallest = left;
    if(right < size && heap[right] < heap[smallest])
        smallest = right;
    
    if (smallest != index)
    { 
        swap(heap[index], heap[smallest]);
        minHeapify(smallest);
    }

}

int removeMin()
{
    if (size <= 0)
        return 0;
    
    if (size == 1)
    {
        size -= 1;
        return heap[0];
    }

    int root = heap[0];
    heap[0] = heap[size -1];
    size -= 1;
    minHeapify(0);

    return root;

}




int main()
{
int n = 0;
scanf("%d", &n);



int* arr2 = malloc(sizeof(int) * (size_t)n);

for(int a = 0; a < n; a ++)
{
    scanf("%d", &arr2[a]);
}

for(int a = 0; a < n; a++)
{
int x = 0;
x = arr2[a]; 
//0 �Է½� �迭�� �ּҰ� �ⷰ, �� �迭 ���� 
// �ڿ��� �Է½ÿ� �迭�� �� �� ����

    if(x == 0)
    {
        if(size == 0) //�ε����� 0 >> ��, �迭�� �ƿ� ����� �ִ� ���
            printf("0\n");
        else//�迭�� ���� �ִ� ���
        {   
            printf("%d\n", heap[0]);
            removeMin();
        }
    }
    if(x > 0)
    {
       insert(x);
    }
}


return 0;

}
```

������ �ð� ������ �����ϸ�, �̴� �ڷᱸ���� ���� �̿��Ͽ� Ǯ��� �Ѵ�. 
�ڵ� ������ �ּ����� �� �ڵ带 ÷���Ѵ�

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#define swap(a, b) do{int temp = a; a = b; b = temp;}while(0)

int heap[100000];
int size = 0;

//size >> �迭�� ���� �ε����̴�. ������������� 0, ���� �ϳ� ������ 1, �� ������ 2......
//�迭�� �ִ� ���̴� x�� �����̴�.
//�迭�� Ȱ�� �ε����� 0��������



int parent(int index)
{ 
    return (index -1) /2;
}

int leftChild(int index)
{ 
    return (index)*2 +1;
}

int rightChild(int index)
{ 
    return (index)*2 + 2;
}

//�ε��� 0���� �����ϴ� �迭-���� parent*2 + 1 > leftchild, parent*2+2 > right chlide,�̴�. 
//(leftchild || right chlild)-1 /2 > parent�̴�. 

void insert(int value)//���� ���ο� ���� �������̴�.
{
    if (size == 9999)
    {}    //���� �� á��
    
    //size�� 9999(��, heap�� ũ�� -1)�̶�°���, ���� �� á�ٴ°��̴�. ��, �Է��� ���� �ʰ� �Ѿ��.


    int index = size;
    heap[size] = value;
    size ++;

   //index���� insert�ϱ� ���� size, size���� insert�� ���� size�� ����ִ�.
   //insert�� index�� �κп� �Ͽ����� - heap�� ���� �� �κп� �־�����- index�������� ���� �ö󰡸鼭 �ּ����� �����ϴ��� �˻��Ѵ�.
   //index�� ������ ������ ������, �˻�ܰ迡�� size�� �����ؾ��ϹǷ�, index�� ������ �����Ͽ� index�� size�� �־���

    while ((index != 0) && (heap[parent(index)] > heap[index])) //�˻簡 ������ �ʾ����� -index�� root�� �ƴϸ� - and 
										    //index�� index�� parent�� �ּ��� ���ǿ� �´� ��쿡 �˻��Ѵ� 
    {
        swap(heap[index], heap[parent(index)]); //while���� ����� �����̹Ƿ� index�� ���� �� parent�� ���� �ٲ��� �ϰ�
        index = parent(index);//index�� �� parent�� �ٲپ �˻縦 ����Ѵ�.
    }


}


//remove�Ŀ� �ּ��� ������ �����ϱ� ���� ������ �Լ� - remove���� ���� �־���Ѵ�!

void minHeapify(int index)
{
    int left = leftChild(index);
    int right = rightChild(index);
    int smallest = index;

    if (left < size && heap[left] < heap[smallest])
        smallest = left;
    if(right < size && heap[right] < heap[smallest])
        smallest = right;


//right <size, left<size�� ���ؼ� right�� left�� heap�� ������ ���� �������� �����Ѵ�.

//���� ���ǹ����� ����, index�� �� right, left�� ������ smallest�Ѱ��� smallest�� �� �ִ�.
    
    if (smallest != index)//index�� smallest�� �ƴѰ�� - ��, �ּ����� ������Ű�� �ʴ� ��쿡
    { 
        swap(heap[index], heap[smallest]); //smallest��, index�� ���� �ڹٲٰ�,
        minHeapify(smallest);//��������� �ڹٲ� �� ���� ���� minHeapify�� �����Ѵ�. 
    }

}

//heap�� �ּҸ� �����ϴ� �Լ�-�ּ����̹Ƿ�, ���� ���� ��-�迭�� �ε���0�� �����ϰԵȴ�.

int removeMin()
{
    if (size <= 0)
        return 0;
    //size�� 0 ���� > ������ ������ ����̰�, 0�ΰ��� ���� �ƹ��͵� ���ٴ°��̴�    

    if (size == 1)
    {
        size -= 1;
        return heap[0];
    }

   //size�� 1>heap�� ���� �ϳ��� �ִٴ°�, heap[0]�� �� ������ ���̹Ƿ� size -=1 �� �ϰ� heap[0]�� �����Ѵ�

    int root = heap[0];
    heap[0] = heap[size -1];
    size -= 1;
    minHeapify(0);
    return root;

//�� ���� ��� > heap[0]�� �����ϰ�, heap�� ���� �� ���� heap[0]���� ��������, size -= 1�� �ϰ�, 0 �������� minheapify�� �����Ѵ�.
 
}




int main()
{
int n = 0;
scanf("%d", &n);



int* arr2 = malloc(sizeof(int) * (size_t)n);

for(int a = 0; a < n; a ++)
{
    scanf("%d", &arr2[a]);
}

for(int a = 0; a < n; a++)
{
int x = 0;
x = arr2[a]; 
//0 �Է½� �迭�� �ּҰ� �ⷰ, �� �迭 ���� 
// �ڿ��� �Է½ÿ� �迭�� �� �� ����

    if(x == 0)
    {
        if(size == 0) //�ε����� 0 >> ��, �迭�� �ƿ� ����� �ִ� ���
            printf("0\n");
        else//�迭�� ���� �ִ� ���
        {   
            printf("%d\n", heap[0]);
            removeMin();
        }
    }
    if(x > 0)
    {
       insert(x);
    }
}


return 0;

}
```

����