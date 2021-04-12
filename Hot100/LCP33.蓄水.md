# LCP33 蓄水

## 题目描述

给定 N 个无限容量且初始均空的水缸，每个水缸配有一个水桶用来打水，第 i 个水缸配备的水桶容量记作 bucket[i]。小扣有以下两种操作：

+ 升级水桶：选择任意一个水桶，使其容量增加为 bucket[i]+1
+ 蓄水：将全部水桶接满水，倒入各自对应的水缸每个水缸对应最低蓄水量记作 vat[i]，返回小扣至少需要多少次操作可以完成所有水缸蓄水要求。

注意：实际蓄水量 达到或超过 最低蓄水量，即完成蓄水要求。

**示例1**

> 输入：`bucket = [1,3], vat = [6,8]`
>
> 输出：4
>
> ![vat1.gif](https://cdn.jsdelivr.net/gh/cy3432412/images//img-120210412110901.gif)

## 题解

总体思路，枚举倒水次数，计算倒水量，选出 最小的次数

~~~java
public int storeWater(int[] bucket, int[] vat) {
        //特判vat为0情况
        int max = 0;
        for(int v:vat)
            if(max < v) max = v;
        if(max == 0) return 0;

        int n = bucket.length;
        int ans = Integer.MAX_VALUE;
        //枚举倒水次数
        for(int i = 1; i <= 10000; i++) {
            int per = 0;
            int cur = i;//倒水i次，所以操作次数+i
            //遍历每一个水缸
            for(int j = 0; j < n; j++) {
                //水槽容量/倒水次数 =  每次倒水量
                per = vat[j] % i == 0 ? vat[j] / i : vat[j] / i + 1;
                // 每次倒水量-初始水量=需要升级次数
                cur += Math.max(0, per - bucket[j]);
            }
            //所有倒水次数中，取最小的操作次数
            ans = Math.min(ans, cur);
        }
        return ans;
}
~~~

