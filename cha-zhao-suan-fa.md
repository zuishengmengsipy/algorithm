# 查找算法

### 顺序查找

```text
int SequenceSearch(int a[], int value, int n)
{
    for(int i=0; i<n; i++)
        if(a[i]==value)
            return i;
    return -1;
}
```

### 二分查找

传统方式，非递归

```text
int BinarySearch1(int a[], int value, int n)
{
    int low, high, mid;
    low = 0;
    high = n-1;
    while(low<=high)
    {
        mid = (low+high)/2;
        if(a[mid]==value)
            return mid;
        if(a[mid]>value)
            high = mid-1;
        if(a[mid]<value)
            low = mid+1;
    }
    return -1;
}
```

递归版本

```text
int BinarySearch2(int a[], int value, int low, int high)
{
    if(low > high)
        return -1;
    int mid = (low+high)/2;
    if(a[mid]==value)
        return mid;
    if(a[mid]>value)
        return BinarySearch2(a, value, low, mid-1);
    if(a[mid]<value)
        return BinarySearch2(a, value, mid+1, high);
}
```

