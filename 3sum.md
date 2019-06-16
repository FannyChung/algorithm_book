# 3sum

n个数字的数组中，找到所有满足条件的三元组，三个元素的和为0



思路

1 先对数组排序。对ai，向右找和为0-ai的（ai&lt;=0\)。找和为ai的方法是对遍历每个值，然后进行二分查找。复杂度为O\(N\*N\*logN\)

2。 排序+hash：先对数组排序。对ai，向右找和为0-ai的（ai&lt;=0\)。找和的方法是建立带坐标的hashmap，耗费时间为O\(N\*logd）其中d是相同的值的个数。总的时间复杂度是O\(N\*N\*logd\)

3。 hash：先两两求和，用hashmap记录和以及他们的坐标。然后对每个值，在map中检查是否有0-ai的和，并要求下标都不一样。最后利用对三个值进行排序来去重。复杂度为O\(N\*N\*9\).——在N=3000的时候，还是超时



正确的方法：

**最重要的是跳过重复的值**

如果ai==a\[i-1\]，则可以不处理ai。

如果aj和a\[j-1\]相同，则同理也不处理。

**双指针法**：对每个i，在右侧找到和为目标的j和k，找的方法是二分查找。碰到相等的i、j、k则跳过。

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    Arrays.sort(nums);
    for (int i = 0; i + 2 < nums.length; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) {              // skip same result
            continue;
        }
        int j = i + 1, k = nums.length - 1;  
        int target = -nums[i];
        while (j < k) {
            if (nums[j] + nums[k] == target) {
                res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                j++;
                k--;
                while (j < k && nums[j] == nums[j - 1]) j++;  // skip same result
                while (j < k && nums[k] == nums[k + 1]) k--;  // skip same result
            } else if (nums[j] + nums[k] > target) {
                k--;
            } else {
                j++;
            }
        }
    }
    return res;
}
```

根据上述思路，对方法3的map中的重复sum（sum是由两个相同的值相加而成的），则可以跳过；如果ai==a\[i-1\]，则可以不处理ai。

