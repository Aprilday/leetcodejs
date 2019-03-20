# 第15题
先简单说说一开始的思路吧
两个循环，第一个每次拿出一个数，从第二个循环里找和第一个循环当前数相加为0的两个数，这两个数的第一个就是内层循环的当前数，方法是定义了一个对象，把相加为0需要的数放入对象，然后判断内层循环后面的数有没有和对象里的key相同的，有就算找到一个。
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
                    // 这里判断的原因是防止后面有符合条件的相同的数
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
看了下其他人的思路，就写了第二版程序，思路还是外层一个个循环，内层从数组最左边和最右边同时计算，根据和外层循环数的和大小移动数组指针。出乎我意料的是，这个方法和上面的方法我在本地测试，性能相差了几十倍，关于这点，还得多思考思考。
'''
var threeSum = function(nums) {
    var len = nums.length
    var res = []
    var l = 0
    var r = 0
    var temp = 0
    
    if (len < 3) {
        return []
    }
    nums.sort((a, b) => a - b)
    
    for(let i = 0; i < len; i++) {
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue
        }
        l = i + 1
        r = len - 1
        temp = -nums[i]
        while (l < r) {
            if (nums[l] + nums[r] > temp) {
                r--
            } else if (nums[l] + nums[r] < temp) {
                l++
            } else {
                res.push([nums[i], nums[l], nums[r]])
                while (l < r && nums[r] === nums[r - 1]) {
                    r--
                }
                while (l < r && nums[l] === nums[l + 1]) {
                    l++
                }
                r -= 1
                l += 1
            }
        }
    }
    return res
};
'''