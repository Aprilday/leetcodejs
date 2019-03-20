# 第15题
先简单说说一开始的思路吧
两个循环，第一个循环每个数，第二个循环里找和第一个循环当前数相加为0的两个数，方法是定义了一个对象，把相加为0需要的数放入对象，然后判断后面的数有没有和对象里的key相同的，有就算找到一个。
```
    var threeSum = function(nums) {
        var len = nums.length
        var res = []
        var temp = {}
        if (len < 3) {
            return []
        }
        nums.sort((a, b) => a - b)

        for(let i = 0; i < len; i++) {
            if (i > 0 && nums[i] === nums[i - 1]) {
                continue
            }
            temp = {}
            for (let j = i + 1; j < len; j++) {
                if (!temp[nums[j]]) {
                    temp[-nums[i] - nums[j]] = 1
                } else {
                    if (temp[nums[j]] === 1) {
                        temp[nums[j]]++
                        res.unshift([nums[i], -nums[i]-nums[j], nums[j]]) 
                    }
                }
            }
        }
        return res
    };

```
但是遗憾的是，这个方法超时，所以还得再接着改进。