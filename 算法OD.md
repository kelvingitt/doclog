1、申请机考后，考试链接会发送到邮箱，发送后我会提醒考试。
2、机考一共三道题，一星难度两道各100分，两星难度一道200分，考试时长150分钟总分400分，累计得分200分即通过，单个考题可以多次提交结果，请根据用例通过率估算得分。
3、机考注意事项（1）：可以在个人IDE编码，练习时本地调试通过复制到网页提交，提前解决环境问题
4、机考注意事项（2）：注意不能在电脑或手机查资料否则会被自动判为作弊。
5、机考注意事项（3）：个人电脑需要摄像头（如果电脑没有摄像头可以准备两个手机，一个手机安装ivcam软件做摄像头，一个用于鉴权），否则机考成绩无效。

温馨提示：
为了机考能有更好的发挥，建议在牛客网上练习一下中低难度的编码题（首页-》在线编程-》华为机试，一共103题），例如字符串、数组、排序、队列、动态规划等
 如下LeetCode题之前考过重点练习一下，可以上LeetCode根据题目编号搜索：
数组：370 531 
字符串： 536 544  
动态规划：651 750 1055 
数学：469 573 
树：536 545 
哈希表：311 314
深搜：505 1059
二分查找：1182
贪心：1055 1057
双指针：360 487
广搜：490 505
栈：439
链表：426
并查集：261
滑动窗口：1100
递归：625
二叉树：1214



数组：370
class Solution:
    def getModifiedArray(self, length: int, updates: List[List[int]]) -> List[int]:
        n = length
        ################ 典型差分，上下台阶的思想，"出租车上下车问题"
        f = [0 for _ in range(n)]   #差分数组
        #### 差分
        for start, end, diff in updates:
            f[start] += diff
            if end + 1 < n:
                f[end + 1] -= diff
        #### 整理
        for i in range(1, n):
            f[i] += f[i-1]
        return f
		
		
class Solution:
    def getModifiedArray(self, length: int, updates: List[List[int]]) -> List[int]:
        f=[0]*length
        for start,end,diff in updates:
            f[start]+=diff
            if diff+1<length:
                f[end]-=diff
        res=[]
        temp=0
        for i in range(1,length):
            f[i]+=f[i-1]
            res.append(f[i])
			
			
import collections
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]

d = collections.defaultdict(int)
for k, v in s:
d[k] += v

print(d.keys())
print(d.values())
print(list(d.items()))

1. 强制规定了dict里面value的值为int，不过不存在就自动赋值0， str赋值“”，list赋值[]

dict赋值 {}

d = collections.defaultdict(int) 这里面的int规定了字典中value值的类型

做统计比较好用， 而且d[k]这样取值不存在不会报错， 默认赋值0（对应类型）

发布于 2020-06-30 19:52
			
数组：531	
Python 哈希表
解题思路
分别统计每行每列有多少黑色像素。然后遍历找到黑色像素查看当前行和当前列是否只有一个黑色像素

代码

class Solution:
    def findLonelyPixel(self, picture: List[List[str]]) -> int:
        row = defaultdict(int)
        comlun = defaultdict(int)
		
        m = len(picture)#行
        n = len(picture[0])#列
        for i in range(m):
            for j in range(n):
                if picture[i][j] == 'B':
                    row[i] += 1
                    comlun[j] += 1
        
        ans = 0
        for i in range(m):
            for j in range(n):
                if picture[i][j] == 'B':
                    if (row[i] ==1 and comlun[j]==1):
                        ans += 1
        return ans

作者：Daxin-2021
链接：https://leetcode-cn.com/problems/lonely-pixel-i/solution/python-ha-xi-biao-by-daxin-2021-ce36/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

class Solution:
    def findLonelyPixel(self, picture: List[List[str]]) -> int:
        row=collections.defaultdict(int)
        col=collections.defaultdict(int)
        
        m=len(picture)
        n=len(picture[0])
        for i in range(m):
            for j in range(n):
                if picture[i][j]=="B":
                    row[i]+=1
                    col[j]+=1
        ras=0
        for i in range(m):
            for j in range(n):
                if row[i]==1 and col[j]==1:
                    ras+=1
        return ras