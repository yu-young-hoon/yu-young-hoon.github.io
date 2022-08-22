---
layout: default
title: algorithm sort 정리
parent: algorithm
nav_order: 405103
---

### 삽입
* 두번째 부터 시작 자신의 왼쪽으로 진행하며 작은것 앞에 삽입, 크면 오른쪽으로 시프트
* t(n) = (n-1) + (n-2) ….. (n-(n-1)) = n*n - (1….(n-1))n = n(n-1)/2 = O(n^2)
```java
void insertion_sort(int list[], int n) {
      int i, j;
      int next;
      for(i = 1; i < n; i++) {                   /*1*/
            next = list[i];
            for(j = i - 1; j >= 0 && next < list[j]; j--) /*2*/
                  list[j + 1] = list[j];
            list[j + 1] = next;
      }
}
```


### 선택
* 최대를 찾고 가장 오른쪽과 교환, 한번 돌면오른쪽은 제외
* t(n) = (n-1) + (n-2) ….. (n-(n-1))
* = n*n - (1….(n-1))n
* = n(n-1)/2
* = O(n^2)
```java
void selection_sort(int *d)
{
  int i,j,t,min;
  for(i=0; i<9; i++)
  { 
 min = i;
     for(j=i+1; j<10; j++)
         { if (d[min]>d[j]) min = j;}
 t=d[i]; d[i]=d[min]; d[min]=t; 
  }
}
```


### 버블
* idx와 idx+1을 비교 큰것을 오른쪽으로 한번 돌면 오른쪽제외


### 머지
* 배열을 반으로 쪼개고 다시 합하면서 정렬
```java
merge_sort(array,0,sizeof(array)/sizeof(int)-1);

void merge_sort(int* array, int start, int end){
if(start>=end) return;

    int mid=(start+end)/2;
 
    merge_sort(array,start,mid);
    merge_sort(array,mid+1,end);
 
    merge(array,start,mid,end);
}
void merge(int* array, int start, int mid, int end){
int* tmp=(int*)malloc(sizeof(int)*(end-start+1));
int tmp_index=0;
int p=start,q=mid+1;
int i;
for(i=tmp_index; i<=end-start; i++){
while(p<=mid && q<=end){
if(array[p]>array[q]){
tmp[tmp_index]=array[q];
q++;
}else{
tmp[tmp_index]=array[p];
p++;
}
tmp_index++;
}
if(p>mid){
while(q<=end){
tmp[tmp_index]=array[q];
q++;
tmp_index++;
}
}
else{
while(p<=mid){
tmp[tmp_index]=array[p];
p++;
tmp_index++;
}
}
}//end for
for(i=start; i<=end; i++){
array[i]=tmp[i-start];
}
free(tmp);
}
```


### 기수
* 최대 값을 찾고 한자리수부터 가장 큰자리수 까지 반복해서 큐에 넣고 뺀다. 큐저장 크기 기록
```java
//< 기수정렬 ( 큐 사용버젼 )
void radixSort_Queue(int* arr, int size)
{
    //< 큐를 사용 ( 버킷수 만큼 )
    queue<int> qu[BUCKET];
    //< 인수
    int factor = 1;
    //< 최대값
    int max = 0;
    //< 정렬 단계 
    int count = 1;
    //< 버킷 인덱스
    int index = 0;
     //< 최대값을구한다.
    for(int i=0; i<size; i++)
    {
        if( arr[i] > max )
        {
            max = arr[i];
        }
    }


//< 최대값자리수만큼반복
while( ( max / factor ) > 0 )
{
//< 자릿수에 따른 배열 데이터를 버킷에 분배
for(int i=0; i<size; i++)
{
index = (arr[i]/factor)%10;
qu[index].push(arr[i]);
}
//< 버킷에 있는 순서대로 배열에 넣기
index = 0;
for(int i=0; i<BUCKET; i++)
{
//< 버킷에 데이터가 존재하면
while(qu[i].empty() == false)
{
//< 버킷에 데이터를 꺼내어 배열에 저장한후 버킷 데이터 삭제
arr[index++] = qu[i].front();
qu[i].pop();
}
}
//< 다음자리수
factor *= 10;
}
}
```


### quik
* 피봇 보다 큰 오른쪽 선택, 피봇 보다 작은 왼쪽 선택, 두개를 교환
* 절반을 재귀적으로 반복해서 정렬
* 모든 요소가 역순일때 O(n^2) 중간 선택으로 개선
```java
int partition(int* arr, int left, int right)
{
	int mid = (left + right) / 2;
	swap(arr, left, mid);

	int pivot = arr[left];
	int i = left, j = right;
	while (i < j)
	{
 		while (pivot < arr[j]) {
		j--;
 	}
while (i < j && pivot >= arr[i]) {
i++;
}
swap(arr, i, j);
}
arr[left] = arr[i];
arr[i] = pivot;
return i;
}

void quicksort(int* arr, int left, int right)
{
if (left >= right)
{
return;
}
int pi = partition(arr, left, right);
quicksort(arr, left, pi - 1);
quicksort(arr, pi + 1, right);
}
```


### 힙정렬
* 힙을 통해서 정렬 우선순위 큐를 만들때도 사용
```java
var Heap = (function() {
  function Heap() {
     this.arr = [];
  }
 function reheapUp(self, idx) {
    if (idx) {
      var parent = parseInt((idx - 1) / 2);
      if (self.arr[idx] > self.arr[parent]) {
        var temp = self.arr[idx];
        self.arr[idx] = self.arr[parent];
        self.arr[parent] = temp;
        reheapUp(self, parent);
      }
    }
  }
 function reheapDown(self, idx) {
    var left = 0;
    var right = 0;
    var large;
    if (idx * 2 + 1 < self.arr.length) {
      left = self.arr[idx * 2 + 1];
      if (idx * 2 + 2 < self.arr.length - 1) {
        right = self.arr[idx * 2 + 2];
      }
      if (left > right) {
        large = idx * 2 + 1;
      } else {
        large = idx * 2 + 2;
      }
      if (self.arr[idx] < self.arr[large]) {
        var temp = self.arr[idx];
        self.arr[idx] = self.arr[large];
        self.arr[large] = temp;
        reheapDown(self, large);
      }
    }
  }

Heap.prototype.insert = function(number) {
var last = this.arr.length;
this.arr[last] = number;
reheapUp(this, last);
return true;
};
Heap.prototype.delete = function() {
if (this.arr.length === 0) {
return false;
}
var del = this.arr[0];
this.arr[0] = this.arr.pop();
reheapDown(this, 0);
return del;
};
Heap.prototype.sort = function() {
var sort = [];
var count = this.arr.length;
for (var i = 0; i < count; i++) {
sort.push(this.delete());
}
return sort;
};
return Heap;
})();
```


### 카운팅 정렬
```java
int main(){
    int N,A[MAX_SIZE+1];
    int B[MAX_SIZE+1];
    int count[MAX_NUM+1];
    int countSum[MAX_NUM+1]; // 수열 길이 N은 MAX_SIZE. 
    scanf(""%d"",&N); // count배열을 모두 0으로 초기화 
    for(int i=0;i<=N;i++)
        count[i]=0; //수열 A에 입력되는 수는 MAX_NUM 
    for(int i=1;i<=N;i++){
        scanf(""%d"",&A[i]); //숫자 등장 횟수 세기 
        count[A[i]]++;
    } //누적합 구성 
    countSum[0]=count[0];
    for(int i=1;i<=MAX_NUM;i++)  //뒤에서부터 수열 A 순회
        countSum[i]=countSum[i-1]+count[i];
    for(int i=N;i>=1;i--)
        B[countSum[A[i]]]=A[i];countSum[A[i]]--;
    //수열 A를 정렬한 결과인 수열 B를 출력한다. 
    for(int i=1;i<=N;i++)
        printf(""%d"",B[i]);
}
```
