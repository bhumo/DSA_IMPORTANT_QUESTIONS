# Merge Sort

Algorithm

1. Calculate mid
2. Call merger Sort on left part(start,mid)
3. Call mergeSort on right part (mid+1,end)
4. finally merge those two sorted part of the same array

This way we will recursively break the array into two parts until we reach the point where there are only two blocks left. We won't be going to the part where s==e because that would mean we are trying to sort the part where there is only one element  left. And s>e is incorrect as we have moved out of scope for the given range of \[s,e]



TC: nlogn

SC: n (the last merge)

```
//Merge Sort
#include<iostream>
using namespace std;

void mergeSortedArray(int *arr,int s,int e){
    int mid = s + (e-s)/2;
    int left_start = s;
    int left_end = mid;
    int right_start = mid +1;
    int right_end = e;
    int* left_array = new int[left_end-left_start+1];
    int* right_array = new int[right_end-right_start+1];
    int j = 0;
    //copying the original value of the left part of the array into left_array
    for(int i=left_start;i<=left_end;i++){
        left_array[j]=arr[i];
        j++;
    }
    j =0;
    //copying the original value of the right part of the array into right_array
    for(int i=right_start;i<=right_end;i++){
        right_array[j] = arr[i];
        j++;
    }
    int left_array_size = left_end - left_start + 1;
    int right_array_size = right_end - right_start +1;
    int i=0;
    j=0;
    int k = left_start;
    while(i<left_array_size && j<right_array_size){
        if(left_array[i]<right_array[j]){
            arr[k] = left_array[i];
            i++;
            k++;
        }else{
            arr[k] = right_array[j];
            j++;
            k++;
        }
    }

    while(i<left_array_size){
        arr[k] = left_array[i];
        i++;
        k++;
    }

    while(j<right_array_size){
        arr[k] = right_array[j];
        j++;
        k++;
    }

    delete []left_array;
    delete []right_array;
}
void mergeSort(int *arr,int s,int e){
    if(s>=e){
        return;
    }

    int mid = s + (e-s)/2;

    mergeSort(arr,s,mid);
    mergeSort(arr,mid+1,e);
    mergeSortedArray(arr,s,e);

}

int main(){
    cout<<"Enter the size of array:";
    int n;
    cin>>n;

    int *arr = new int[n];
    for(int i=0;i<n;i++){
     cin>>arr[i];   
    }
    mergeSort(arr,0,n-1);
    for(int i=0;i<n;i++){
        cout<<arr[i]<<" ";
    }
    cout<<endl;
    return 0;
}
```
