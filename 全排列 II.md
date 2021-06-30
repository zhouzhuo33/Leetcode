给定一个可包含重复数字的序列 `nums` ，**按任意顺序** 返回所有不重复的全排列。

 

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

解析：回溯

```c++
class Solution
{
public:
    vector<vector<int>> res;
    vector<int> path;
    vector<bool> used;
    void backtrack(vector<int> &nums, int depth)
    {
        if (depth == nums.size())
        {
            res.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); i++)
        {
            // used[i] 是判断是否使用过了，后面的：这个判断条件保证了对于重复数的集合，一定是从左往右逐个填入的
            //即去重,使相同字段排列只有一种
            if (used[i] || i > 0 && nums[i] == nums[i - 1] && !used[i - 1])
                continue;
            path.push_back(nums[i]);
            used[i] = true;
            backtrack(nums, depth + 1);
            used[i] = false;
            path.pop_back();
        }
    }
    vector<vector<int>> permuteUnique(vector<int> &nums)
    {
        sort(nums.begin(), nums.end());
        used.resize(nums.size());
        backtrack(nums, 0);
        return res;
    }
};
```

