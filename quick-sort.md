# Quick sort

```
#include<iostream>
using namespace std;
int partition (int arr[], int start, int end)
{
   // Your code here 
   int pivotElement = arr[start];
   int count  = 0;
   for(int i=start+1;i<=end;i++){
       if(arr[i]<=pivotElement) count++;
   }
   int pivotCorrectPosition = start + count;
   swap(arr[start],arr[pivotCorrectPosition]);
   
  int i = start;
   int j = end;
   while(i<pivotCorrectPosition && j>pivotCorrectPosition ){
       while(arr[i]<=pivotElement) i++;
       while(arr[j]>pivotElement) j--;
       if(i<j){
           swap(arr[i],arr[j]);
           i++;
           j--;
       }
   }
   
   return pivotCorrectPosition;
}
void quickSort(int arr[], int start, int end)
{
    // code here
    if(start>=end) return;
    int partitionIndex = partition(arr,start,end);
    
    quickSort(arr,start,partitionIndex-1);
    quickSort(arr,partitionIndex+1,end);
}
int main(){

    int arr[]={24,18,38,43,14,40,1,54};
    int n = 8;
    quickSort(arr,0,n-1);
    for(int i=0;i<n;i++){
        cout<<arr[i]<<" ";
    }
    cout<<endl;

    return 0;
}
```
