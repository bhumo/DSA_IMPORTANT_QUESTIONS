# Count Inversion

Find the count inversion for the given array



Approach: Merge sort

We know that inversion, arr\[i]>arr\[j]&#x20;

so we will make use of merge sort,&#x20;

LOGIC: whenever we make the swap that is when arr\[j]\<arr\[i] at that time, we can say a\[j] is smaller than i -> left_array_size and it can be added to the solution

TC: O(nlogn)

SC: O(n)

&#x20;



```
#include<iostream>
using namespace std;

    long long int merge(long long arr[],long long s, long long e){
    long long mid = s + (e-s)/2;
    long long left_start = s;
    long long left_end =  mid;
    long long right_start = mid+1;
    long long right_end = e;
    long long left_array_size = left_end - left_start +1;
    long long right_array_size = right_end - right_start +1;
    long long* left_array = new long long[left_array_size];
    long long* right_array = new long long[right_array_size];
    long long k = s;
    
    for(long long i=0;i<left_array_size;i++){
        left_array[i]=arr[k];
        k++;
    }
    for(long long i=0;i<right_array_size;i++){
        right_array[i]=arr[k];
        k++;
    }
    
    long long i = 0;
    long long j = 0;
     k = left_start;
        long long int count =0;
    while(i<left_array_size && j<right_array_size){
        if(left_array[i]<=right_array[j]){
    
            arr[k]=left_array[i];
            i++;
            k++;
        }else{

            arr[k]=right_array[j];
            count += (left_array_size-i);
            j++;
            k++;
        }
    }
    
    while(i<left_array_size){
        arr[k]=left_array[i];
        k++;
        i++;
    }
    
    while(j<right_array_size){
        arr[k]=right_array[j];
        j++;
        k++;
    }
    delete []left_array;
    delete []right_array;
    return count;
}
long long int mergeSort(long long arr[],long long s,long long e){
    if(s >= e) return 0;
    long long int count_inversion = 0;
    long long mid = s + (e-s)/2;
     count_inversion += mergeSort(arr,s,mid);
    count_inversion += mergeSort(arr,mid+1,e);
    count_inversion += merge(arr,s,e);
    return count_inversion;
}

    long long int inversionCount(long long arr[], long long N)
    {
        // Your Code Here
        return mergeSort(arr,0,N-1);
    }

int main(){
    long long arr[] = {4,5,2,1,8,7,10};
    long long n = 7;
    cout<<inversionCount(arr,n-1);
    return 0;
}
```
