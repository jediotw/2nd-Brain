
**1.Factorial of a number** 
```
N!=N*(N-1)*(N-2)*....*1
3!=3*2*1

def recursion(n);
	if n==1;
		return 1;
	else:
		return n*recursion(n-1);
```

**2.Linear Search**
```
def sqrt(n);
	for i in range(n):
		if i*i==n:
			return i;
		
```

**3.Binary Search**
```
def sqrt(n):
	int start=0
	int high=n
	while(start<=high){
		int mid=start+(high-start)/2
		if mid*mid==n:
			return mid
		if mid*mid>n:
			high=mid-1;
		else:
			start=mid+1;
	}
```

**4.Fibonacci Sequence**
	*0 1 1 2 3 5 8 13*
```
def fib(n):
	if n==0:
		return 0
	if n==1:
		return 1
	return fib(n-1)+fib(n-2)
```

**4.1Fibonacci Sequence with DP**

```
def fib(n,notebook={}){

//befor hand look if n is already availble in notebook to avoid calc
	if n in notebook:
		return notebook[n];
	//if not available go ahead
	if n==0:
		return 0
	if n==1:
		return 1;
	//store the answer
	ans=fib(n-1)+fib(n-2)
	//finally store the answer in notebook
	notebook[n]=ans;
	//return the answer
	return ans;
	
}
```

**4.1.2 Fibonacci Sequence with iterative approach**
```
|Variable a|Variable b|
|----------|----------|
| b        | a+b      |

```
```
def fib(n):
	a=0
	b=1
for i in range(n):
	a,b=b,a+b
	return a
```

**5.Reversing a List using stack**
```
def rev(nums):
	ans=[]
while(len(nums)>0):
	ans.append(nums.pop());
return ans
```

**6.Venn Diagram**

| Notation  | Operation Name         | Meaning                                              |
| --------- | ---------------------- | ---------------------------------------------------- |
| A ∩ B     | Intersection           | Common elements in both A and B                      |
| A ∪ B     | Union                  | All elements from both A and B, excluding duplicates |
| A ⋂ B = ∅ | Disjoint Sets          | No common elements between A and B                   |
| A △ B     | Symmetric Difference   | Elements in A or B but **not** in both               |
| A - B     | Difference (A minus B) | Elements in A **not** in B                           |
| B - A     | Difference (B minus A) | Elements in B **not** in A                           |
| A ⊆ B     | Subset                 | All elements of A are also elements of B             |

**7.Check if all the characters are unique or not?**
```
def unique(s):
	set=set()
for i in s:
//if already in set
	if i in set:
		return false
	//else add in set
	st.add(i)
return true

2nd method
def unique(s):
	st=set(list(s))
return len(st)==len(s)
```
8.Binary tree
```
if depth(d) if given of a complete binary tree the total number of nodes=2^d-1 
```
```
0 1 2 3 4 5 
for a perfect binary tree the left child is at index=2*index+1
for a perfect binary tree the right child is at index=2*index+2
```


**8.BFS uses queue**
### 📚 **How it works:**

1. Start from a **source node**.
2. Use a **queue** to keep track of nodes to visit.
3. Mark nodes as **visited** to avoid repetition.
4. Visit all neighbors of the current node.
5. Repeat until the queue is empty.

```
def bfs(graph,start){
visited=set()
queue=deque([start])

while queue:
	node=queue.popleft()

	if node not in visited:
		print(node)
		visited.add(node)

	for neighbor in graph[node]:
		if neighbor not in visited:
			queue.append(neigbor)

}
```


**9.Palindrome**
```
1.method 1

def palindrome(s):
	return rev(s)==s
	
2.method 2

def isPalindrome(s);
	ans=""
	for i in s:
		ans+=i;
	return ans; or just return s[::-1]==s
	
3.two pointer approach

	def isPalindrome(s):
    left = 0
    right = len(s) - 1

    while left <= right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True


```

**10.Two sum** 
```
def twosum(num,t):
	sz=len(num)
	for i in range(sz):
		for j in range(i):
			if num[i]+num[j]==t:
				return true
	return false
```
```
def twosum(num,t):
	notebook=set()
	for (target-i) in notebook:
		return true
	nb.add(i)
	return false
```
```
def twosun(num,t):
	num.sort() //for reverse num.sort(reverse=True)
	left=0
	right=len(num)-1
	while(left<=right):
		if num[left]+num[right]==t:
			return True
		if num[left]+num[right]<t:
			left+=1
		else:
			right-=1
	return False
	
```

**11.Inverse Factorial**
```

factorial
3!=1*2*3

Inverse Factorial
invfact(0)=-1
invfact(1)=1
invfact(2)=2
invfact(24)=4
invfact(6)=3
invfact(7)=-1

if 1*2*3*4 > n then we cannot find inverse factorail 
			==n then we can find it
```

**12.Sum of Digits**
```
def sumDigits(num):
    ans = 0
    while num > 0:
        ans += num % 10
        num //= 10
    return ans

```
```
def sumDigit(num):
    if num == 0:
        return 0
    return num % 10 + sumDigit(num // 10)

```
```
def sumDigitStr(num):
    ans = 0
    s = str(num)
    for i in s:
        ans += int(i)
    return ans

```

**13.Anagram**
```
def Anagram(s1,s2):
	a1={}
	a2={}
	for i in s1:
		if i in a1:
			a1[i]+=1
		else:
			a1[i]=1

	for i in s2:
		if i in a2:
			a2[i]+=1
		else:
			a2[i]=1
	return a1==a2
	
```
```
from collections import Counter

def anagram(s1, s2):
    a1 = Counter(s1)
    a2 = Counter(s2)
    return a1 == a2

```
```
from collections import Counter

def anagram(s1, s2):
    d1=deafultdict(int)
    d2=defaultdict(int)
    for i in s1:
	    d1[i]+=1
	for i in s2:
		d2[i]+=1
return d1==d2

```

**14.GCD and LCM**
```
Given Two Numbers a,b
LCM=(a*b)/GCD(a,b)


def gcd(a,b):
	while b>0:
		a,b=b,a%b
return a

def lcm(a,b):
	return  (a*b)/gdc(a,b)
```
15.Median 
```
1. if total numbers are odd then sort the numbers and  pick the middle element as median
2. else sort the numbers and then take average of two middle number the average is the median of the numbers
def median(nums):
	nums.sort()
	sz=len(nums)
	if sz%2==1:
		return nums[sz//2]
	else:
	return (nums[n//2]+nums[n//2-1])/2
	
```

**16.Jump Game using BFS and DFS**
- [ ] ⏳ 2025-04-07 Learn it again 

**17.Merge Sort**
```
def merge(left, right):
    merged = []
    i = j = 0

    # Merge the sorted halves
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            merged.append(left[i])
            i += 1  # Python doesn't support i++ syntax
        else:
            merged.append(right[j])
            j += 1

    # Add remaining elements from left, if any
    while i < len(left):
        merged.append(left[i])
        i += 1

    # Add remaining elements from right, if any
    while j < len(right):
        merged.append(right[j])
        j += 1

    return merged

def mergeSort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left_half = mergeSort(arr[:mid])
    right_half = mergeSort(arr[mid:])

    return merge(left_half, right_half)
```
18.Merge Two Sorted List
```
def merge(a,b):
	c=a+b;
	c.sort()
	return c
```
19.Quick Sort
```
1.pick any number from the given numbers as pivot or last element
2.Rearrange the list such that all elements smaller than the pivot are on the left, and all elements greater than the pivot are on the right.
3.Recursively sort the left and right sub-arrays.

def quick_sort(arr):
	if len(arr)<=1:
		return arr

//choose pivot
	pivot=arr[-1]//last element or pivot=random.choice(num)
// Step 2: Partition the list into left, equal, and right based on the pivot
	left=right=equal=[]
	for num in arr:
		if num<pivot:
			left.append(num)
		elif num>pivot:
			right.append(num)
		else:
			equal.append(num)
return quick_sort(left)+equal+quick_sort(right)	

```
20.List in Python
```
[from:to] to is not included
functions are
1.append()
2.sum()
3.len()
4.Max()
5.Min()

```
21.Check a Valid Parentheses of a string
```
def valid(s):
    b = 0
    for i in s:
        if i == "(":
            b += 1
        elif i == ")":
            b -= 1
        if b < 0:
            return False  
    return b == 0  
```
22.Min Number of Brackets Needed to Make a Valid Parentheses String
```
def repair(s):
	b=0
	ans=0
		for i in s:
			if i=="(":
				b+=1
			elif i==")":
				b-=1
				if(b<0):
					bal=0;
					ans+=1
	return ans+bal
```
23 Enhanced Valid Parentheses String Algorithm using a Stack
```
def valid(s):
    st = []
    for i in s:
        # If it's an opening bracket, push it to the stack
        if i in ["(", "[", "{"]:
            st.append(i)
        # If it's a closing bracket, check for matching opening bracket
        elif i in [")", "]", "}"]:
            if len(st) == 0:  # If the stack is empty, no matching opening bracket
                return False
            # Directly compare the last item in the stack with the current closing bracket
            if i == ")" and st[-1] != "(":
                return False
            if i == "]" and st[-1] != "[":
                return False
            if i == "}" and st[-1] != "{":
                return False
            st.pop()  # Remove the matched opening bracket
    # If the stack is empty, all brackets were matched, otherwise not
    return len(st) == 0


```
**24.Binary Search Tree**
##### 1.Left Subtree < root> Right Subtree

```
class Tree:
	def __init__(self,val,left,right):
		self.val=val
		self.left=left
		self.right=right
	def BST(root,val):
	
		if root is None:
			return False
			
		if(val==root.val):
			return True
			
		if val<root.val:
			BST(root.left,val)
		
		return BST(root->right,val)
2.Method Iterative
	def BST(root,val):
	
		while root is not None:
			if val==root.val:
				return True
			if val<root.val:
				root=root.left
			else:
				root=root.right
		//if after this we cannot find the value so return false
		return false

Note: Skewed Tree takes O(n) while balanced takes o(logn)
```
25.Validate BST
```
def Validate(root,min,max):
	if root is None:
		retrun True
	if root.val<min or root.val>max:
		return false
	return Validate(root.left,min,root.val) and Validate(roo.right,root.val,max)
```

`26.Binary Tree Traversal

## DFS Types
#### NLR-preorder
#### LNR-In Order
#### LRN-Post Order


```
def inorder(root):
	if root is None:
		return
	inorder(root.left)
	print(root.val)
	inorder(root.right)

```
Note:
In order of BST gives Sorted Numbers
Time Complexity is O(n) and space complexity because of Recursion O(n)

27.Count the number of nodes in binary tree
```
Using DFS

def count(root):
	if root is None:
		return 0
	return count(root.left)+count(root.right)
```
```

Using BFS

def count(root):
	if root is None:
		return 0
	ans=0
	q=[root]
	while len(q)>0:
		p=q.pop(0)
		ans+=1
		if p.left:
			q.append(p.left)
		if p.right:
			q.append(p.right)
	return ans
```

28.Binary to Decimal Conversion
```
def bin2dec(b):
	ans=0
	for digit in b:
		ans= ans*2+int(digit)
	return ans
//ans= ans*2 move one position left and int(digit) add one digit 
like 2*10=20
	20*10=200
	200*10=2000
	like wise for binary also
```

29.Interval Intersection

- For the starting points we need to find the max of both the starting points 
- whereas, for the ending points we need to find min of both the ending points
```
given Intervals=[[5,7],[3,10]]
def intervalIntersection(intervals):
	if len(Intervals)==0:
		return None
	left,right=Intervals[0][0],Intervals[0][1]
	for Interval in Intervals:
		left=max(left,Interval[0])
		right=min(right,Interval[1])
		if left>=right:
			return None
	return [left,right]
```

30.Prefix Sum to calculate Interval sums
```
//prefix template
def prefixsum(nums):
	prefix=[0]
	sum=0
	for i in nums:
		sum+=nums[i]
		prefix.append(sum)
	
```


```
def sumInterval(from,to):
	return prefix[to+1]-prefix[from]
```

31.Linked List (ToDo)
```
class Node:
		def __init__(self,val,next=None)
		self.val=val
		self.next=next
	def addNode(self,val):
		newNode=Node(val)
		self.next=newNode
		return newNode
```

32.Fast and Slow Pointer to find middle of the linked list
```
def detect_cycle(root):
    slow = fast = root
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

```

**Programs in GO lang from Now**
33.Heap and Priority Queue
- heap is a complete binary tree
- 
```
import heapq as pq
q=[1,3,4,5,6]
pq=heapify(q)->O(n)
pq.heappop(q)->O(logn)
pq.heappush(q,7) ->O(logn)
pq.replace ->pop the smallest element and push the new element


```
```
import heapq as hq
data=[1,2,3]
hq.heapify(data)
hq.heappush(data,4)
hq.heappush(data,5)
n=hq.nlargest(2,data) ➤ Get the 2 largest elements** from the `data` list
m.hq.nsmallest(3,data) ➤ Get the 3 smallest elements** from the `data` list.

print(n)
print(m)
```

34.Minimum cost to connect stick
```
import heapq as hq

def minimumCostToConnectSticks(arr):
    cost = 0
    hq.heapify(arr)
    
    while len(arr) > 1:
        a = hq.heappop(arr)
        b = hq.heappop(arr)
        total = a + b
        cost += total
        hq.heappush(arr, total)
    
    return cost

```

35.Graph
**Note**
- A graph can have cycle but tree cannot have cycle
- tree, binary tree ,linked list and list are graph
- if edges are weighted we call it weighted graph
- by default in unweighted graph edges are of 1 weight
- if edges have direction called directed graph

36.Palindrome permutation
- if odd char/num count is greater than one than we cannot build palindrome 
- for a 3 digit number or 3 length string we have 3 choices for 1st place,2 choice for second place,1 choice for 3rd place so we call it 3!. As we can use first digit in three places like wise if one digit is occupied then we left with 2 choices and so on and so forth.
- if num%2== 1 is equal to if num&1== 1
```
from collections import Counter

def palindromeString(s):
    d = Counter(s)
    odd_count = 0

    for i in d.keys():
        if d[i] % 2 == 1:
            odd_count += 1
        if odd_count > 1:
            return False
    return True

```

**37.Binary Search to Compute the Logarithm Base Two Function**
- Monotonic(mono-single) means when x increases y also increases
- Bitonic Array
```
 Logb (mn) = n logb m
```
def binary_log2(n):
    low, high = 0, n
    epsilon = 1e-6

    while high - low > epsilon:
        mid = (low + high) / 2
        power = 2 ** mid

        if power < n:
            low = mid
        else:
            high = mid

    return low  # or (low + high) / 2

```
- In integer binary search, you can say `while low <= high` because values are exact.
    
- But in floating point binary search, never match exactly — they keep getting closer (e.g., 4.000001, 4.0000001, ...).
    
- So instead of equality, we check if they're "close enough" using `epsilon`.
- `epsilon` is a very small number, e.g., `1e-6` or `0.000001`.
```

38.Reverse Linked List using recursion and iterative method
- [ ] 🔽 ➕ 2025-04-09 
 39.Remove elements from Linked List
 - [ ] 📅 2025-04-09 ⏬ 
 40.Sqrt using binary search
 ```
def sqrt(x):
    if x < 0:
        return None  # Square root of negative number is not real

    if x == 0 or x == 1:
        return x

    # Set the precision
    epsilon = 1e-6

    # Define search space
    left, right = (x, 1) if x < 1 else (0, x)

    while abs(curr - x) > epsilon:
        mid = (left + right) / 2
        curr = mid * mid

        if curr < x:
            left = mid
        else:
            right = mid

    return mid

```

41 Pythagorean Theorem and Algorithm to Find Pythagorean Numbers
- [ ] 📅 🔽 
42.Double Ended Queue
```
from collections import dequeue
q=dequeue()
q.append(1)
q.append(2)
q.appendleft(3)
q.pop()
q.popleft()

```
43 Double-Ended Queue to Perform a BFS to Sum Nodes in a Tree

```
def sumofTree(root):
	if root is None:
		return 0
	ans=0
	q.append(root)
	while len(q)>0:
		p=q.popfront()
		ans+=p.val
		if p.left:
			q.append(p.left)
		if q.left:
			q.append(p.right)
	return ans
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

    def add_left_child(self, value):
        self.left = Node(value)
        return self.left

    def add_right_child(self, value):
        self.right = Node(value)
        return self.right

# Creating the tree
root = Node(1)
root.add_left_child(2)
right = root.add_right_child(3)
right.add_left_child(4)
right.add_right_child(5)

```
44.pascal triangle
```
def pascal(rows,cols):
	if row==0 or cols==0 or row==cols:
		return 1
	return pascal(r-1,c)+pascal(r-1,c-1)
```
