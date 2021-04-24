### 顺序表相关知识简单记录
#### C顺序表的静态分配
```C
#include<stdio.h>
#include<stdlib.h>

#define MaxSize 50

typedef struct{
    int data[MaxSize];
    int length;
}SqList;


int main(){
    SqList L;
    L.length=0;
    for(int i=0;i<51;++i){
        if(i>=MaxSize){
            break;
        }else{
            L.data[i]=i;
            L.length++;
        }
    }
    printf("%d\n",L.length);
    for(int i=0;i<MaxSize;++i){
        printf("%d\n",L.data[i]);
    }
    return 0;
}
```
#### C顺序表的动态内存分配和扩容
```C
#include<stdio.h>
#include<stdlib.h>

#define InitSize 50

typedef struct{
    int* data;
    int MaxSize,length;
}SqList;


int main(){
    SqList L;
    L.data=(int*)malloc(sizeof(int)*InitSize);
    L.MaxSize=InitSize;
    L.length=0;
    for(int i=0;i<51;++i){
        L.length++;
        L.data[i]=i;
        if(L.length==L.MaxSize){
            SqList temp;
            L.data=(int*)realloc(L.data,sizeof(int)*InitSize*(L.MaxSize/InitSize+1));
            L.MaxSize=InitSize*(L.MaxSize/InitSize+1);
        }
    }
    printf("%d\n",L.length);
    for(int i=0;i<51;++i){
        printf("%d\n",L.data[i]);
    }
    return 0;
}
```
#### C++顺序表的动态分配及扩容
```C++
#include<bits/stdc++.h>
using namespace std;

#define InitSize 50

typedef struct{
    int* data;
    int MaxSize,length;
}SqList;


int main(){
    SqList L;
    L.data=new int[InitSize];
    L.MaxSize=InitSize;
    L.length=0;
    for(int i=0;i<51;++i){
        L.length++;
        L.data[i]=i;
        if(L.length==L.MaxSize){
            SqList temp;
            temp.data=new int[InitSize*(L.MaxSize/InitSize+1)];
            memcpy(temp.data,L.data,sizeof(int)*L.MaxSize);
            L.MaxSize=InitSize*(L.MaxSize/InitSize+1);
            delete[] L.data;
            L.data=temp.data;
        }
    }
    for(int i=0;i<51;++i){
        printf("%d\n",L.data[i]);
    }
    return 0;
}
```