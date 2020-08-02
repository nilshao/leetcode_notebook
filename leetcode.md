冒泡算法
```c++
class Solution {
public:
    int partition(vector<int>& nums, int l, int r) {
        int pivot = nums[r];
        int i = l - 1;
        for (int j = l; j <= r - 1; ++j) {
            if (nums[j] <= pivot) {
                i = i + 1;
                swap(nums[i], nums[j]);
            }
        }
        swap(nums[i + 1], nums[r]);
        return i + 1;
    }
    int randomized_partition(vector<int>& nums, int l, int r) {
        int i = rand() % (r - l + 1) + l; // 随机选一个作为我们的主元
        swap(nums[r], nums[i]);
        return partition(nums, l, r);
    }
    void randomized_quicksort(vector<int>& nums, int l, int r) {
        if (l < r){
            int pos = randomized_partition(nums, l, r);
            randomized_quicksort(nums, l, pos - 1);
            randomized_quicksort(nums, pos + 1, r);
        }
    }

    vector<int> sortArray(vector<int>& nums) {
        srand((unsigned)time(NULL));
        randomized_quicksort(nums, 0, (int)nums.size() - 1);
        return nums;
    }


};
```

```C++
//string字符串数字转换为int，包括负数情况
    int to_int(string str_num){
            int point=0;
            int flag =1;
            if(str_num[0]=='-') flag=-1;
            for(char i:str_num){
                if(i=='-')  continue;
                point =point*10+(i-'0');
            }
            point*=flag;
            return point;
        }
//维护一个单调递增栈
    stack<int> find_increase_stack(vector<int>& nums){
        stack<int> res; //返回res
        stack<int> tmp; 
        //两种特殊情况
        if(nums.size()==0)  return res;
        else if(nums.size()==1){
            res.push(nums[0]);
        }
        //两个元素以上
        else{
            for(int num: nums){         //遍历所有vector nums中的数字                
                while(!res.empty()){
                    if(num>res.top())   break;  //如果是最大就直接跳出到入栈操作
                    else{
                        tmp.push(res.top());    //把更大的数现暂存至tmp栈
                        res.pop();
                    }
                }
                res.push(num);                  //放入当前数值
                while(!tmp.empty()){            //把tmp栈中数字压回去
                    res.push(tmp.top());
                    tmp.pop();
                }
            }
        }
        return res;

//求根节点到某节点路径
    //main函数里已知或自定义变量
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p){
        //已知根节点root，找p
        vector<TreeNode*> pathp;
        vector<TreeNode*> path;
        int finish_flag = 0;
        findpath(root,p,path,pathp,finish_flag);
        //最后得到的pathp是想要的路径
        return blabla;
    }

    void findpath(TreeNode* node, TreeNode* target, vector<TreeNode*> &path, vector<TreeNode*> &path_target, int &flag){
        //node是正在遍历的节点，target，path遍历时的节点路径栈
        //最后节点存在path_target里面
        //flag：最终是否搜索到，找到变1
        if(!node||flag)   return ;  //node为空或者已经找到节点
        path.push_back(node);
        if(node==target){
            flag =1;
            path_target = path;
        }
        findpath(node->left, target, path,path_target,flag);
        findpath(node->right, target, path,path_target,flag);
        path.pop_back();
        
    }
//检测int 数字变成二进制之后有多少个1
    //把一个整数减去1，再与原整数相与，会把原整数的最右边的1变成0
    int  NumberOf1(int n) {
          //把一个整数减去1，再与原整数相与，会把原整数的最右边的1变成0
         int cnt = 0;
         while(n){
             cnt++;
             n=n&(n-1);
         }
         return cnt;
     }
//最大公约数
    int gcd(int x, int y){
        return !x ? y : gcd(y % x, x);
    }
```

```C++
//判断是否质数函数
    bool isPrimer(int n){
	    bool flag = true;
	    if (n<2) flag = false;
	    for (int i=2; i*i<=n;i++){
		    if (n%i==0) {
			    flag = false;
			    break;
		    }	
	    }
	return flag;
    }
```

```C++
//字母变大小写
    统一转成大写：ch & 0b11011111 简写：ch & 0xDF
    统一转成小写：ch | 0b00100000 简写：ch | 0x20··
```