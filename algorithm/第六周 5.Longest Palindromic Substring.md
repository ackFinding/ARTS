### 5.Longest Palindromic Substring
**思路**：使用Manacher算法，算出中心和回文半径。  
如果直接根据算法中点C有可能被改变，需要在max改变才更新中点C。也可以不要realC,去掉步骤1，直接只在max<=radius[i]才更新C和R，但不知道为啥运行更慢。
```java
class Solution {
    
public char[] manacherString(String str) {
    char[] orgin = str.toCharArray();
    char[] res = new char[orgin.length * 2 + 1];
    int index = 0;
    for (int i = 0; i < res.length; i++) {
        res[i] = (i & 1) == 0 ? '#' : orgin[index++];
    }
    return res;
}
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 1) {
            return "";
        }
        char[] mana = manacherString(s);
        int C = -1;
        int max = Integer.MIN_VALUE;
        int R = -1;
        int[] radius = new int[mana.length];
        int realC = 0;
        for (int i = 0; i < mana.length; i++) {
            radius[i] = R > i ? Math.min(R - i, radius[2 * C - i]) : 1;
            while (i + radius[i] < mana.length && i - radius[i] > -1) {
                if (mana[i + radius[i]] == mana[i - radius[i]]) {
                    radius[i]++;
                } else {
                    break;
                }
            }
            //1.
            if (i + radius[i] > R) {
                R = i + radius[i];
                C = i;
            }
            if (max<=radius[i]){
                max = radius[i];
                realC = i;
            }
        }
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = realC - (radius[realC] - 1); i < realC + (radius[realC] - 1) && i>-1; i++) {
            if ((i & 1) != 0) {
                stringBuilder.append(mana[i]);
            }
        }
        return stringBuilder.toString();
    }
}
```
