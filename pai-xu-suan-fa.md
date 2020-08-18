# 排序算法

冒泡排序

```text
function bubbleSort(arr) {
    varlen = arr.length;
    for(vari = 0; i < len - 1; i++) {
        for(varj = 0; j < len - 1 - i; j++) {
            if(arr[j] > arr[j+1]) {        // 相邻元素两两对比
                vartemp = arr[j+1];        // 元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    returnarr;
}
```

#### 2、选择排序（Selection Sort） <a id="2&#x9009;&#x62E9;&#x6392;&#x5E8F;selection-sort"></a>

```text
function selectionSort(arr) {
    varlen = arr.length;
    varminIndex, temp;
    for(vari = 0; i < len - 1; i++) {
        minIndex = i;
        for(varj = i + 1; j < len; j++) {
            if(arr[j] < arr[minIndex]) {     // 寻找最小的数
                minIndex = j;                 // 将最小数的索引保存
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    returnarr;
} 
```

#### 3、直接插入排序（Insertion Sort） <a id="3&#x63D2;&#x5165;&#x6392;&#x5E8F;insertion-sort"></a>

```text
function insertionSort(arr) {
    varlen = arr.length;
    varpreIndex, current;
    for(vari = 1; i < len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while(preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    returnarr;
}
```

折半插入排序

```text
void BinSort(int *a,int n) //对int数组进行从小到大的排序 
{
	for(int i=1;i<n;i++) //开始 以a[0]作为有序序列，从a[1]开始找到当前元素a[i]应该放置的位置 
	{
		int low=0,high = i-1,mid;//每次寻找a[i]的位置，都要更新这些数据 
		while(low<=high) //二分思想循环寻找a[i]的位置 
		{
			mid = (low+high) / 2;  
			if(a[i]<=a[mid])
				high = mid - 1;  //high指针减小 
			else
				low = mid + 1;   //low指针增加 
		}  //循环结束，low就是a[i]应该放置的位置 
		
		int temp = a[i];  
		for(int j=i;j>low;j--)  //将元素向后平移
			a[j] = a[j-1];  
		a[low] = temp;   //将元素temp = a[i] 放置到low位置 
	}
}
```

希尔排序

书上更好





快速排序

```text
function quickSort(arr, left, right) {
    varlen = arr.length,
        partitionIndex,
        left = typeofleft != 'number'? 0 : left,
        right = typeofright != 'number'? len - 1 : right;
 
    if(left < right) {
        partitionIndex = partition(arr, left, right);
        quickSort(arr, left, partitionIndex-1);
        quickSort(arr, partitionIndex+1, right);
    }
    returnarr;
}
 
function partition(arr, left ,right) {     // 分区操作
    varpivot = left,                      // 设定基准值（pivot）
        index = pivot + 1;
    for(vari = index; i <= right; i++) {
        if(arr[i] < arr[pivot]) {
            swap(arr, i, index);
            index++;
        }       
    }
    swap(arr, pivot, index - 1);
    returnindex-1;
}
 
function swap(arr, i, j) {
    vartemp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

