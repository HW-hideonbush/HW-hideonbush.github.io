# 栈

给定一个整数数组 `A`，*坡*是元组 `(i, j)`，其中 `i < j` 且 `A[i] <= A[j]`。这样的坡的宽度为 `j - i`。

找出 `A` 中的坡的最大宽度，如果不存在，返回 0 。

 

**示例 1：**

```
输入：[6,0,8,2,1,5]
输出：4
解释：
最大宽度的坡为 (i, j) = (1, 5): A[1] = 0 且 A[5] = 5.
```

**示例 2：**

```
输入：[9,8,1,0,1,9,4,0,4,1]
输出：7
解释：
最大宽度的坡为 (i, j) = (2, 9): A[2] = 1 且 A[9] = 1.
```

```
 class Solution {

public:
  int maxWidthRamp(vector<int>& A) {
   	int ans=0;
    stack<pair<int,int>> sta;
    for(int i=0;i<A.size();i++){
    	///维护一个栈，栈里是比栈顶元素小的项
    	///[6,0,8,2,1,5]
    	///6 0 
      if(sta.empty()||(A[i]<sta.top().first)) sta.push(make_pair(A[i],i));
    }
    for(int i=A.size()-1;i>=0;i--){
    	///
        while(!sta.empty()&&A[i]>=sta.top().first){
            ans=max(ans,i-sta.top().second);
            sta.pop();
        }
    }
    return ans;
  }

};
```

