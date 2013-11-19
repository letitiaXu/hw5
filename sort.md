## 必须掌握
+ 冒泡排序
+ 选择排序
+ 插入排序
+ 快速排序
+ 归并排序

以上排序最常用，也是面试必考。  
考试惯例会有一题排序，但出的形式不一定，有可能专门考某个排序的原理细节。所以大家以上都要理解。  


### 冒泡排序
**原理：** 相邻两个元素如不符合大小顺序立即交换。

    for (int i = 0; i < n; i++)
		for (int j = 1; j < n - i; j++)
		if (a[j - 1] > a[j])
			swap(a[j - 1], a[j]);


### 选择排序
**原理：** 从最右（最左开始），一个个地把剩下数列中最大（最小）的数与当前数列最右（最左）元素交换。

	for (int i = 0; i < n; i++) {
		int k = i;
        for (int j = i + 1; j < n; j++) {
			if (a[k] > a[j]) {
				k = j;
                total++;
            }
        }

        if (k != i) {
            int temp = a[k];
            a[k] = a[i];
            a[i] = temp;
        }
	}

### 插入排序
**原理：** 对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

    for (int i = 1; i < n; i++) {
        int k = a[i];
        for (int j = i; j > 0 && k < a[j-1]; j--)
            a[j] = a[j-1];
        a[j] = k;
    }

##  快速排序
**原理：** 分治法思想。选取一个主元（一般取中间或者随机取），通过交换的方式保证主元左边比主元小，右边比主元大。（逆序就相反）

    void sort(int l,int r) {
        int i=l,j=r,x=a[(i+j)/2];
        do {
            while (x>a[i]) i++;
            while (x<a[j]) j--;
            if (i<=j) {
				int t=a[i];
                 a[i]=a[j];
                 a[j]=t;
                 i++;j--;         
            }
         } while(i<=j);
         if (i<r) sort(i,r);
         if (l<j) sort(l,j);     
    }

### 归并排序
**原理：** 分治法思想。两个有序数列合并成一个有序数列的复杂度为O（N），归并就是不停地把数列二分拆成两个数列，直到只剩一个数，此时两个数的排序就很容易了。然后从底部再排完序返回来逐渐合并有序序列。

	void merge(int s1, int e1, int s2, int e2) {
        int i = s1, j = s2;
        int cnt = s1;

        while (cnt <= e2) {
            if ((j > e2 || a[i] <= a[j]) && i <= e1) {
                b[cnt] = a[i];
                cnt++;
                i++;
            }
            else if ((i > e1 || a[i] > a[j]) && j <= e2){
                b[cnt] = a[j];
                cnt++;
                j++;
            }
        }
    
        for (int i = s1; i <= e2; i++)
            a[i] = b[i];
    }

    void merge_sort(int l, int h) {
        if (h - l <= 1) {
            if (a[l] > a[h])
                swap(a[l], a[h]);
            return;
        }

        int mid = (h + l) / 2;
        merge_sort(l, mid);
        merge_sort(mid + 1, h);

        merge(l, mid, mid + 1, h);
    }
