# [1824. Minimum Sideway Jumps](https://leetcode.com/problems/minimum-sideway-jumps)

[中文文档](/solution/1800-1899/1824.Minimum%20Sideway%20Jumps/README.md)

## Description

<p>There is a <strong>3 lane road</strong> of length <code>n</code> that consists of <code>n + 1</code> <strong>points</strong> labeled from <code>0</code> to <code>n</code>. A frog <strong>starts</strong> at point <code>0</code> in the <strong>second </strong>lane<strong> </strong>and wants to jump to point <code>n</code>. However, there could be obstacles along the way.</p>

<p>You are given an array <code>obstacles</code> of length <code>n + 1</code> where each <code>obstacles[i]</code> (<strong>ranging from 0 to 3</strong>) describes an obstacle on the lane <code>obstacles[i]</code> at point <code>i</code>. If <code>obstacles[i] == 0</code>, there are no obstacles at point <code>i</code>. There will be <strong>at most one</strong> obstacle in the 3 lanes at each point.</p>

<ul>
	<li>For example, if <code>obstacles[2] == 1</code>, then there is an obstacle on lane 1 at point 2.</li>
</ul>

<p>The frog can only travel from point <code>i</code> to point <code>i + 1</code> on the same lane if there is not an obstacle on the lane at point <code>i + 1</code>. To avoid obstacles, the frog can also perform a <strong>side jump</strong> to jump to <strong>another</strong> lane (even if they are not adjacent) at the <strong>same</strong> point if there is no obstacle on the new lane.</p>

<ul>
	<li>For example, the frog can jump from lane 3 at point 3 to lane 1 at point 3.</li>
</ul>

<p>Return<em> the <strong>minimum number of side jumps</strong> the frog needs to reach <strong>any lane</strong> at point n starting from lane <code>2</code> at point 0.</em></p>

<p><strong>Note:</strong> There will be no obstacles on points <code>0</code> and <code>n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/1800-1899/1824.Minimum%20Sideway%20Jumps/images/ic234-q3-ex1.png" style="width: 500px; height: 244px;" />
<pre>
<strong>Input:</strong> obstacles = [0,1,2,3,0]
<strong>Output:</strong> 2 
<strong>Explanation:</strong> The optimal solution is shown by the arrows above. There are 2 side jumps (red arrows).
Note that the frog can jump over obstacles only when making side jumps (as shown at point 2).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/1800-1899/1824.Minimum%20Sideway%20Jumps/images/ic234-q3-ex2.png" style="width: 500px; height: 196px;" />
<pre>
<strong>Input:</strong> obstacles = [0,1,1,3,3,0]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There are no obstacles on lane 2. No side jumps are required.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/1800-1899/1824.Minimum%20Sideway%20Jumps/images/ic234-q3-ex3.png" style="width: 500px; height: 196px;" />
<pre>
<strong>Input:</strong> obstacles = [0,2,1,0,3,0]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The optimal solution is shown by the arrows above. There are 2 side jumps.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>obstacles.length == n + 1</code></li>
	<li><code>1 &lt;= n &lt;= 5 * 10<sup>5</sup></code></li>
	<li><code>0 &lt;= obstacles[i] &lt;= 3</code></li>
	<li><code>obstacles[0] == obstacles[n] == 0</code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def minSideJumps(self, obstacles: List[int]) -> int:
        f = [1, 0, 1]
        for v in obstacles[1:]:
            g = [inf] * 3
            for j in range(3):
                if v != j + 1:
                    g[j] = f[j]
            if v != 1:
                g[0] = min(g[0], min(g[1], g[2]) + 1)
            if v != 2:
                g[1] = min(g[1], min(g[0], g[2]) + 1)
            if v != 3:
                g[2] = min(g[2], min(g[0], g[1]) + 1)
            f = g
        return min(f)
```

### **Java**

```java
class Solution {
    private int inf = 0x3f3f3f3f;
    
    public int minSideJumps(int[] obstacles) {
        int[] f = new int[] {1, 0, 1};
        for (int i = 1; i < obstacles.length; ++i) {
            int v = obstacles[i];
            int[] g = new int[] {inf, inf, inf};
            for (int j = 0; j < 3; ++j) {
                if (v != j + 1) {
                    g[j] = f[j];
                }
            }
            if (v != 1) {
                g[0] = Math.min(g[0], Math.min(g[1], g[2]) + 1);
            }
            if (v != 2) {
                g[1] = Math.min(g[1], Math.min(g[0], g[2]) + 1);
            }
            if (v != 3) {
                g[2] = Math.min(g[2], Math.min(g[0], g[1]) + 1);
            }
            f = g;
        }
        return Math.min(f[0], Math.min(f[1], f[2]));
    }
}
```

### **C++**

```cpp
class Solution {
public:
    const int inf = 0x3f3f3f3f;

    int minSideJumps(vector<int>& obstacles) {
        vector<int> f = {1, 0, 1};
        for (int i = 1; i < obstacles.size(); ++i) {
            int v = obstacles[i];
            vector<int> g(3, inf);
            for (int j = 0; j < 3; ++j) if (v != j + 1) g[j] = f[j];
            if (v != 1) g[0] = min(g[0], min(g[1], g[2]) + 1);
            if (v != 2) g[1] = min(g[1], min(g[0], g[2]) + 1);
            if (v != 3) g[2] = min(g[2], min(g[0], g[1]) + 1);
            f = move(g);
        }
        return *min_element(f.begin(), f.end());
    }
};
```

### **Go**

```go
func minSideJumps(obstacles []int) int {
	inf := 0x3f3f3f3f
	f := [3]int{1, 0, 1}
	for _, v := range obstacles[1:] {
		g := [3]int{inf, inf, inf}
		for j := 0; j < 3; j++ {
			if v != j+1 {
				g[j] = f[j]
			}
		}
		if v != 1 {
			g[0] = min(g[0], min(g[1], g[2])+1)
		}
		if v != 2 {
			g[1] = min(g[1], min(g[0], g[2])+1)
		}
		if v != 3 {
			g[2] = min(g[2], min(g[0], g[1])+1)
		}
		f = g
	}
	return min(f[0], min(f[1], f[2]))
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```

### **...**

```

```

<!-- tabs:end -->
