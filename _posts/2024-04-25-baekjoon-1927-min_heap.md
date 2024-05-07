---
title:  "백�?? 1927-최소?��"
excerpt: "md ?��?��?�� 마크?��?�� 문법?���? ?��?��?��?�� Github ?���? ????��?��?�� ?��로드 ?��보자. ?��?��?��?�� Visual Studio code ?��?��! 로컬 ?��버에?�� ?��?��?�� ?��보자. "

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git, baekjoon]

toc: true
toc_sticky: true
 
date: 2024-04-25
last_modified_at: 2024-05-06
---

2024-4-35?�� 백�?? 1927-최소?�� 문제�? ????��?��

https://www.acmicpc.net/problem/1927

![image](https://github.com/softkleenex/softkleenex.github.io/assets/92619941/e71e63ee-850f-45a9-a36f-99a5e5c58ea5)


체출?�� ?��?��코드?�� ?��?���? 같다.

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
    {}    //?��?�� �? 찼다
    
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
//0 ?��?��?�� 배열?�� 최소�? 출럭, �? 배열 ?���? 
// ?��?��?�� ?��?��?��?�� 배열?�� �? �? ?��?��

    if(x == 0)
    {
        if(size == 0) //?��?��?���? 0 >> �?, 배열?�� ?��?�� 비워?�� ?��?�� 경우
            printf("0\n");
        else//배열?�� 뭐라?�� ?��?�� 경우
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

문제?�� ?���? ?��?��?�� ?��각하�?, ?��?�� ?��료구조의 ?��?�� ?��?��?��?�� ????��?�� ?��?��. 
코드 ?��명이 주석?���? ?��?���? 코드�? 첨�???��?��

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#define swap(a, b) do{int temp = a; a = b; b = temp;}while(0)

int heap[100000];
int size = 0;

//size >> 배열?�� �??�� ?��?��?��?��?��. 비워?��?��?��?��?�� 0, 값이 ?��?�� ?��?���? 1, ?�� ?��?���? 2......
//배열?�� 최�?? 길이?�� x?�� ?��?��?��?��.
//배열?�� ?��?�� ?��?��?��?�� 0?��?���??��



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

//?��?��?�� 0�??�� ?��?��?��?�� 배열-?��??? parent*2 + 1 > leftchild, parent*2+2 > right chlide,?��?��. 
//(leftchild || right chlild)-1 /2 > parent?��?��. 

void insert(int value)//?��?�� ?��로운 값을 ?��?��?��?��?��.
{
    if (size == 9999)
    {}    //?��?�� �? 찼다
    
    //size�? 9999(�?, heap?�� ?���? -1)?��?��?��것�??, ?��?�� �? 찼다?��것이?��. �?, ?��?��?�� 받�?? ?���? ?��?��간다.


    int index = size;
    heap[size] = value;
    size ++;

   //index?��?�� insert?���? ?��?�� size, size?��?�� insert?�� ?��?�� size�? ?��?��?��?��.
   //insert�? index?�� �?분에 ?��????��?�� - heap?�� �??�� ?�� �?분에 ?��?��?��?��- index?��?���??�� ?���? ?��?���?면서 최소?��?�� 만족?��?���? �??��?��?��.
   //index�? 별도�? ?��?��?�� ?��?��?��, �??��?��계에?�� size�? 번형?��?��?���?�?, index�? 별도�? ?��?��?��?�� index?�� size�? ?��?��?��

    while ((index != 0) && (heap[parent(index)] > heap[index])) //�??���? ?��?���? ?��?��?���? -index�? root�? ?��?���? - and 
										    //index??? index?�� parent�? 최소?�� 조건?�� 맞는 경우?�� �??��?��?�� 
    {
        swap(heap[index], heap[parent(index)]); //while문을 ?��과한 ?��?��?���?�? index?�� 값과 �? parent?�� 값�?? 바�?�어?�� ?���?
        index = parent(index);//index�? �? parent�? 바꾸?��?�� �??���? 계속?��?��.
    }


}


//remove?��?�� 최소?�� 조건?�� ?���??���? ?��?�� ?��?��?�� ?��?�� - remove보다 ?��?�� ?��?��?��?��?��!

void minHeapify(int index)
{
    int left = leftChild(index);
    int right = rightChild(index);
    int smallest = index;

    if (left < size && heap[left] < heap[smallest])
        smallest = left;
    if(right < size && heap[right] < heap[smallest])
        smallest = right;


//right <size, left<size�? ?��?��?�� right??? left�? heap?�� 범위?�� ?��?��??? ?��?��?���? ?��각한?��.

//?��?�� 조건문들?�� ?��?��, index??? �? right, left?�� 값들�? smallest?��것이 smallest?�� ?��?���? ?��?��.
    
    if (smallest != index)//index�? smallest�? ?��?��경우 - �?, 최소?��?�� 만족?��?���? ?��?�� 경우?��
    { 
        swap(heap[index], heap[smallest]); //smallest???, index?�� 값을 ?��바꾸�?,
        minHeapify(smallest);//?���??��?���? ?��바꾼 �? 값에 ????�� minHeapify�? ?��?��?��?��. 
    }

}

//heap?�� 최소�? ?��거하?�� ?��?��-최소?��?���?�?, ?��?�� �??�� ?��-배열?�� ?��?��?��0?�� ?��거하게된?��.

int removeMin()
{
    if (size <= 0)
        return 0;
    //size�? 0 ?��?�� > ?��?��?�� ?��류의 경우?���?, 0?��경우?�� ?��?�� ?��무것?�� ?��?��?��것이?��    

    if (size == 1)
    {
        size -= 1;
        return heap[0];
    }

   //size�? 1>heap?�� 값이 ?��?���? ?��?��?���?, heap[0]?�� �? ?��?��?�� 값이�?�? size -=1 ?�� ?���? heap[0]?�� 리턴?��?��

    int root = heap[0];
    heap[0] = heap[size -1];
    size -= 1;
    minHeapify(0);
    return root;

//�? ?��?�� 경우 > heap[0]?�� 리턴?���?, heap?�� �??�� ?�� 값을 heap[0]?���? �??��?���?, size -= 1?�� ?���?, 0 ?��?���??�� minheapify�? ?��?��?��?��.
 
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
//0 ?��?��?�� 배열?�� 최소�? 출럭, �? 배열 ?���? 
// ?��?��?�� ?��?��?��?�� 배열?�� �? �? ?��?��

    if(x == 0)
    {
        if(size == 0) //?��?��?���? 0 >> �?, 배열?�� ?��?�� 비워?�� ?��?�� 경우
            printf("0\n");
        else//배열?�� 뭐라?�� ?��?�� 경우
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

?��?��!!!!!! 