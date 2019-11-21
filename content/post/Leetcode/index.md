---
title: Jiashuo's LeetCode Exercise
date: 2019-08-15
math: true
diagram: true
markup: mmark
image:
  placement: 3
  caption: 'Image credit: [**John Moeses Bauan**](https://unsplash.com/photos/OGZtQF8iC0g)'
---

### This is a documentation for LeetCodes

## LeetCode 009

```c++
#include <iostream>

using namespace std;
/*Revert the whole number
//Problematic for very large number
bool isPalindrome(int x) {
        if (x < 0) return false;
	int x1 = x;
	int x2 = 0;
	int lastdig = 0;
	while (x != 0) {
		lastdig = x%10;
		x = x/10;
		x2 = x2*10+lastdig; 
	}
	if (x1 == x2) return true;
	else return false;
}
*/

//Revert half of the number
bool isPalindrome(int x) {
	if (x < 0) return false;
	//special case: x = 0 or x = 10;
	if (x > 0 && x%10 == 0) return false;
	int x1 = x;
	int x2 = 0;
	while (x1 > x2) {
	    x2 = x2*10 + x1%10;
	    x1 = x1/10;
	}
	if (x1 == x2) return true;
	if (x2/10 == x1) return true;
	return false;
}


int main() {
	cout << isPalindrome(123321) << endl;	
	return 0;
}
```

## LeetCode 011
```c++
#include <iostream>
#include <vector>

using namespace std;
/*
int calculateArea(int h1, int h2, dis) {
	int h = min(h1,h2);
	int area = h*dis;
	return area;
}
*/	

int maxArea(vector<int>& height) {
	int len = height.size();
	int l = 0;
	int r = len-1;
	int area = 0;
	while (l < r)
	{
		area = max(area, min(height[l],height[r])*(r-l));
		if (height[l]<height[r])
		{
			l++;
		}
		else 
		{
			r--;
		}
	}
	return area;
}

int main(){
	vector<int> sides;
	sides.push_back(1);
	sides.push_back(8);
	sides.push_back(6);
	sides.push_back(2);
	sides.push_back(5);
	sides.push_back(4);
	sides.push_back(8);
	sides.push_back(3);
	sides.push_back(7);
	int Amax = maxArea(sides);
	cout << Amax << endl;
	return 0;
}
```

## LeetCode 017
```c++
#include <iostream>
#include <vector>

using namespace std;

void helper(vector<string> &vec, string str, int nos) {
	if (nos == 0) {
		vec.push_back(str);
		return;
	}
	//Update last digit and remaining number
	int lastdig = nos % 10;
	nos = nos/10;
	//Map the last digit to ASCII values
	//Number 7, 8 and 9 are special cases
	if (lastdig == 7) {
		helper(vec, char(112) + str, nos);
		helper(vec, char(113) + str, nos);
		helper(vec, char(114) + str, nos);
		helper(vec, char(115) + str, nos);
	}
	else if (lastdig == 8) {
		helper(vec, char(116) + str, nos);
		helper(vec, char(117) + str, nos);
		helper(vec, char(118) + str, nos);
	}
	else if (lastdig == 9) {
		helper(vec, char(119) + str, nos);
		helper(vec, char(120) + str, nos);
		helper(vec, char(121) + str, nos);
		helper(vec, char(122) + str, nos);
	}
	else {
		int ascii1 = 3*lastdig+91;
		int ascii2 = 3*lastdig+92;
		int ascii3 = 3*lastdig+93;
		//Convert the ASCII values to characters
		//Run the recursion function helper until the condition nos = 0 is met
		helper(vec, char(ascii1) + str, nos);
		helper(vec, char(ascii2) + str, nos);
		helper(vec, char(ascii3) + str, nos);
	}
}

//Encounted error (solved): terminate called after throwing an instance of 'std::invalid_argument'
//what():  stoi
//Never forget to consider trivial cases
vector<string> letterCombinations(string digits) {
	vector<string> combos;
	if (digits == "") {}
	else {
		int numbers = std::stoi(digits);
		helper(combos, "", numbers);
	}
	return combos;
}

int main() {
	vector<string> letcoms = letterCombinations("");
	for (vector<string>::iterator it = letcoms.begin(); it != letcoms.end(); ++it) {
		cout << *it<< " ";
	}
	cout << "\n";
	return 0;
}

```

## LeetCode 021
```c++  
// Header file for input output functions 
#include<iostream>  

using namespace std; 

 // Definition for singly-linked list.
/*
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};
*/

#include "ListNode.h"


ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* c1 = l1;
    ListNode* c2 = l2;
    ListNode* curr = NULL;
    ListNode* Merged = NULL;
    
    if (l1 == NULL && l2 == NULL) {return NULL;}
    if (l1 == NULL && l2 != NULL) {return l2;}
    if (l1 != NULL && l2 == NULL) {return l1;}
    if (l1->val <= l2->val) {
        Merged = new ListNode(l1->val);
        curr = Merged;
        c1 = c1->next;
    }
    else {
        Merged = new ListNode(l2->val);
        curr = Merged;
        c2 = c2->next;
    }
    while (c1 != NULL && c2 != NULL) {
        cout << "Reached Here1" << endl;

        if (c1->val <= c2->val){
            cout << "Reached Here2" << endl;
 	    ListNode* NewNode = new ListNode(c1->val);
	    curr->next = NewNode;
            c1 = c1->next;            
        }
        else {
	    curr->next = new ListNode(c2->val);
            c2 = c2->next; 
 	}
        curr = curr->next;
    }
    if (c1 == NULL) {
        while (c2 != NULL){
            curr->next = new ListNode(c2->val);
            c2 = c2->next;
            curr = curr->next;
        }
    }
    else if (c2 == NULL) {
        while (c1 != NULL){
            curr->next = new ListNode(c1->val);
            c1 = c1->next;
            curr = curr->next;
        }
    }
    return Merged;
}


ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
	ListNode* h1 = l1;
	ListNode* h2 = l2;
	ListNode* h1t = NULL;
	ListNode* h2t = NULL;
	ListNode* head;
	int smaller;
	if (h1 == NULL)
	{
		return h2;
	}
	if (h2 == NULL)
	{
		return h1;
	}
	if (h2->val < h1->val)
	{
		head = h2;
		h2t = h2;
		h2 = h2->next;
		h2t->next = h1;
		smaller = 1;
	}
	else
	{
		head = h1;
		h1t = h1;
		h1 = h1->next;
		h1t->next = h2;
		smaller = 0;
	}
	while (h1!=NULL and h2!=NULL)
	{
		if (smaller == 1)
		{
			if (h2->val < h1->val)
			{
				h2t->next = h2;
				h2t = h2;
				h2 = h2->next;
				h2t->next = h1;
			}
			else
			{
				h1t = h1;
				h1 = h1->next;
				h1t->next = h2;
				smaller = 0;
			}
		}
		else
		{
			if (h1->val < h2->val) 
			{
				h1t->next = h1;
				h1t = h1;
				h1 = h1->next;
				h1t->next = h2;
			}
			else
			{
				h2t = h2;
				h2 = h2->next;
				h2t->next = h1;
				smaller = 1;
			}
		}
	}
	return head;
}

// main function -0 
// where the execution of program begins 
int main() 
{ 
    //Build two lists, l1 and l2
    ListNode* l1 = new ListNode(1);
    ListNode* second1 = new ListNode(2);
    ListNode* third1 = new ListNode(4);
    l1->next = second1;
    second1->next = third1;

    ListNode* l2 = new ListNode(1);
    ListNode* second2 = new ListNode(3);
    ListNode* third2 = new ListNode(4);
    l2->next = second2;
    second2->next = third2;
    
    ListNode* MergedList = mergeTwoLists(l1,l2);
    for (ListNode* i = MergedList; i != NULL;) {
        cout << i->val << endl;
        i = i->next;
    }
    return 0;
} 
```
## LeetCode 022
```c++
// Simple C++ program to display "Hello World" 
  
// Header file for input output functions 
#include <iostream>
#include <vector>
using namespace std; 

//NOTE: Must use ALIASING here.
void helper (vector<string> &vec, string s, int p, int q, int n) {
	if (q == n) {
		vec.push_back(s);
		cout << "Pushed string is " << s << endl;
		cout << "Vector address is " << &vec << endl;
		cout << "Vector size is " << vec.size() << endl;
		return;
	}
	
	/*WRONG_METHOD: 
	if (p == q && p < n) {
		cout << "IF1: " << "p = " << p << ", q = " << q << endl;
		helper(vec, s + "(", p + 1, q, n);
	}
	else if (p == q && p == n) {
		cout << "IF2: " << "p = " << p << ", q = " << q << endl;
		helper(vec, s + ")", p, q + 1, n);	
	}
	else {
		cout << "IF3: " << "p = " << p << ", q = " << q << endl;
		helper(vec, s + "(", p + 1, q, n);
		helper(vec, s + ")", p, q + 1, n);
	}
	*/
	
	if (p < n) {
		cout << "p = " << p << " < " << "n = " << n << endl;
		cout << s << endl;
		helper(vec, s + "(", p + 1, q, n);
	}
	if (q < p) {
		cout << "q = " << q << " < " << "p = " << p << endl;
		cout << s << endl;
		helper(vec, s + ")", p, q + 1, n);	
	}
}

vector<string> generateParentheses(int n) {
	vector<string> vectstr;
	helper(vectstr, "", 0, 0, n);
	return vectstr;
}

void print(vector<string> const &input) {
	for (int i = 0; i < input.size(); i++) {
		std::cout << input.at(i) << " ";
	}
	return;
}

int main () {
	vector<string> paracombo = generateParentheses(3);
	print(paracombo);
	return 0;
}

```
## LeetCode 023
```c++

```
## LeetCode 024
```c++
#include <iostream>
using namespace std;

struct ListNode {
	int val;
	ListNode *next;
	ListNode(int x) : val(x), next(NULL) {}
};


ListNode* swapPairs(ListNode* head) {
	cout << "Address of head1 is " << &head << endl;
	//Never use this statement
	//head == NULL ! head->next == NULL:	
	if (head == NULL) {
		return head;
	}
	if (head->next == NULL) {
		return head;
	}
	ListNode* curr1 = head;
	ListNode* curr2 = curr1->next;
	head = curr2;
	ListNode* temp;
	while (curr2->next!=NULL && curr2->next->next!=NULL) {
		curr1->next = curr2->next->next;
		temp = curr2->next;
		curr2->next = curr1;
		curr1 = temp;
		curr2 = temp->next;	
	}
	if (curr2->next == NULL) {
		curr2->next = curr1;
		curr1->next = NULL;
	}
	else if (curr2->next->next == NULL) {
		temp = curr2->next;
		curr2->next = curr1;
		curr1->next = temp;
		temp->next = NULL;
		
	}
	return head;
}


void printList(ListNode* head) {
	cout << "Address of head2 is " << &head << endl;
	ListNode* curr = head;	
	while(curr != NULL) {
		cout << curr->val << " ";
		curr = curr->next;
	}
	cout << endl;
	return;

}

int main() {
	ListNode* headNode = NULL;
	cout << "Address of headNode is " << &headNode << endl;
	headNode = new ListNode(1);
	//headNode->next = new ListNode(2);
	//headNode->next->next = new ListNode(3);
	//headNode->next->next->next = new ListNode(4);
	printList(headNode);
	ListNode* swappedList = swapPairs(headNode);
	//printList(swappedList);
}

```
## LeetCode 025
```c++
#include <iostream>
using namespace std;

struct ListNode {
 	int val;
	ListNode *next;
	ListNode(int x) : val(x), next(NULL) {}
};

//Read carefully what the question is asking you to do
ListNode* reverseKGroup(ListNode* head, int k) {
	if (head == NULL) return head;
        if (k == 0 | k == 1) return head;
	//Find size of list
	ListNode* curr = head;
	int sz = 0;
	while(curr != NULL) {
		curr = curr->next;
		sz += 1;
	}
	cout << "Size is " << sz << endl;
	ListNode* curr1 = head;
	ListNode* curr2 = curr1->next;
	ListNode* temphead = head;
	for (int j=0; j<k-1; j++) {
		head = head->next;
	}
	ListNode* temp;
	if (k > sz) k = sz;
	int n = sz/k;
	for (int i=0; i<n; i++) {
		for (int j=0; j<k-1; j++) {
			temp = curr2->next;
			curr2->next = curr1;
			curr1 = curr2;
			curr2 = temp;		
		}
		/*Modify this part
		temphead->next = curr2;
		curr1 = curr2;
		curr2 = curr2->next;
		temphead = temphead->next;
		*/
	}
	cout << "curr1 is " << curr1->val << endl;	
	cout << "curr2 is " << curr2->val << endl;
	cout << "temp is " << temp->val << endl;
	return head;
}


void printList(ListNode* head) {
	ListNode* curr = head;	
	while(curr != NULL) {
		cout << curr->val << " ";
		curr = curr->next;
	}
	cout << endl;
	return;

}

int main() {
	ListNode* headNode = NULL;
	headNode = new ListNode(1);
	headNode->next = new ListNode(2);
	headNode->next->next = new ListNode(3);
	headNode->next->next->next = new ListNode(4);
	headNode->next->next->next->next = new ListNode(5);
	headNode->next->next->next->next->next = new ListNode(6);
	headNode->next->next->next->next->next->next = new ListNode(7);
	headNode->next->next->next->next->next->next->next = new ListNode(8);
	printList(headNode);
	int K = 3;
	ListNode* reversedList = reverseKGroup(headNode, 3);
	printList(reversedList);
}

```
## LeetCode 035
```c++
#include <iostream>    
#include <vector>

using namespace std;

int searchInsert(vector<int>& nums, int target) {
	int spano = 0;
	vector<int>::iterator it;
	for (it = nums.begin(); it != nums.end(); it++) {
		if (target <= *it) {
			break;
		}
		spano += 1;
	}
	return spano;
}

int main() {
	vector<int> array;
	array.push_back(2);
	array.push_back(3);
	array.push_back(3);
	array.push_back(4);
	array.push_back(5);
	array.push_back(6);
	array.push_back(6);
	array.push_back(7);
	int pos = searchInsert(array, 5);
	cout << pos <<endl;
	return 0;
}

```
## LeetCode 070
```c++
#include <iostream>

using namespace std;

//Using Combinations
/*
int climbStairs(int n) {
	if (n == 0) return 0;
	int ways = 1;
	int denominator = 1;
	int nominator = 1;
	int m = 0;
	for (int i = 1; i < n/2+1; i++)
	{
		m = (i < n-i) ? i : n-i;
		for (int j = 0; j < m; j++)
		{
			denominator *= n-i-j;
			nominator *= i-j;
		}
		ways += denominator/nominator;
		denominator = 1;
		nominator = 1;
	}
	return ways;
}
*/

//Dynamic Programming

int climbStairs(int n)
{
	if (n == 0)
		return 0;
	if (n == 1)
		return 1;
	int step[n+1];
	step[0] = 1;
	step[1] = 1;
	for (int i = 2; i <= n; i++)
	{
		step[i] = step[i-1] + step[i-2];
	}
	return step[n];
}


//Brute force
/*
int climb_stairs(int i, int n)
{
	if (i > n)
	{
		return 0;
	}
	if (i == n)
	{
		return 1;
	}
	return climb_stairs(i+1, n) + climb_stairs(i+2, n);
}

int climbStairs(int n)
{
	return climb_stairs(0,n);
}
*/




int main()
{
	cout << climbStairs(44) << endl;
	return 0;
}
```

## LeetCode 101
```c++
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

///Iterative Method

bool isSymmetric(TreeNode* root) 
{
	if (root == NULL) return true;
	
	queue<TreeNode*> q;
	
	q.push(root);
	q.push(root);
	
	while (!q.empty()) {
		TreeNode* leftNode = q.front();
		q.pop();
		TreeNode* rightNode = q.front();
		q.pop();
		
		cout << leftNode->val << " " << rightNode->val <<endl;
		if (leftNode->val!=rightNode->val) return false;
				
				
		if (leftNode->left!=NULL & rightNode->right!=NULL) 
		{
			q.push(leftNode->left);
			q.push(rightNode->right);
		}
		
		else if (leftNode->left!=NULL | rightNode->right!=NULL)
		{
			return false;
		}
		
		if (rightNode->left!=NULL & leftNode->right!=NULL)
		{
			q.push(rightNode->left);
			q.push(leftNode->right);
		}

		else if (rightNode->left!=NULL | leftNode->right!=NULL)
		{
			return false;
		}
	}
	
	return true;
}

int main() {
	TreeNode* rt = new TreeNode(0);
	rt->left = new TreeNode(1);
	rt->right = new TreeNode(1);
	rt->left->left = new TreeNode(3);
	rt->left->right = new TreeNode(4);
	rt->right->right = new TreeNode(3);
	rt->right->left = new TreeNode(4);
		
	
	vector<int> numList;
	bool is = isSymmetric(rt);
	cout << "The Tree is symmetric?" << is << endl;
	return 0;

}


```

## LeetCode 102
```c++
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct TreeNode {
	int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

/*
vector<vector<int>> levelOrder(TreeNode* root) 
{
	vector<vector<int>> traversal;
	queue<TreeNode*> q;
	vector<int> children;
	if (root == NULL) return vector<vector<int>>();
	q.push(root);
	children.push_back(root->val);
	traversal.push_back(children);
	
	while (!(q.empty())) 
	{
		children = vector<int> ();
		int sz = q.size();
		cout << endl;
		for (int i=0; i<sz; i++)
		{
			TreeNode* currNode = q.front();
			q.pop();
			
			if (currNode->left != NULL) 
			{
				q.push(currNode->left);
				children.push_back(currNode->left->val);
			}
			if (currNode->right != NULL) 
			{
				q.push(currNode->right);
				children.push_back(currNode->right->val);
			}
		} 
		if (!children.empty())
        {
            traversal.push_back(children);
        }
	}
	return traversal;
}
*/

void helper(TreeNode* subroot, vector<vector<int>> &traversal, int index)
{
	if (subroot == NULL) return;
	if (index > traversal.size()) 
		traversal.push_back(vector<int>());
	helper(subroot->left,traversal,index+1);
	traversal[index-1].push_back(subroot->val);
	helper(subroot->right,traversal,index+1);
}

vector<vector<int>> levelOrder(TreeNode* root) 
{
	vector<vector<int>> level_order;
	helper(root,level_order,1);
	return level_order;
}


int main() {
	TreeNode* rt = new TreeNode(1);
	rt->left = new TreeNode(2);
	rt->right = new TreeNode(3);
	rt->left->left = new TreeNode(4);
	rt->right->left = new TreeNode(6);
	rt->right->right = new TreeNode(7);

    vector<vector<int>> TVS = levelOrder(rt);
	
	for (int i=0; i<TVS.size(); i++)
	{
		for (int j=0; j<TVS[i].size(); j++)
		{
			cout << TVS[i][j] << " ";
		}
		cout << endl;
	}
	
	return 0;
}
```

## LeetCode 103
```c++
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

struct TreeNode {
	int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};


/*Iterative Method
vector<vector<int>> zigzagLevelOrder(TreeNode* root) 
{
	vector<vector<int>> traversal;
	stack<TreeNode*> s1;
	stack<TreeNode*> s2;
	vector<int> children;
	if (root == NULL) return vector<vector<int>>();
	s1.push(root);
	int reverse = 0;
	while (!(s1.empty() & s2.empty())) 
	{
		children = vector<int>();
		int sz1 = s1.size();
		int sz2 = s2.size();
		TreeNode* currNode;
		if (reverse%2 == 0) {
			for (int i = 0; i < sz1; i++)
			{
				currNode = s1.top();
				s1.pop();
				children.push_back(currNode->val);
				if (currNode->left != NULL) 
				{
					s2.push(currNode->left);
				}
				if (currNode->right != NULL) 
				{
					s2.push(currNode->right);
				}
			}
		}
		else {
			for (int i = 0; i < sz2; i++)
			{
				currNode = s2.top();
				s2.pop();
				children.push_back(currNode->val);
				if (currNode->right != NULL)
				{
					s1.push(currNode->right);
				}
				if (currNode->left != NULL)
				{
					s1.push(currNode->left);
				}
			}
		}
		traversal.push_back(children);
		reverse += 1;
	}
	return traversal;
}
*/

void helper(TreeNode* subroot, vector<vector<int>> &traversal, int index)
{
	if (subroot == NULL) return;
	if (index > traversal.size()) 
		traversal.push_back(vector<int>());
	helper(subroot->left,traversal,index+1);
	if (index%2 == 1)
		traversal[index-1].push_back(subroot->val);
	else
		traversal[index-1].insert(traversal[index-1].begin(),subroot->val);
	helper(subroot->right,traversal,index+1);
}

vector<vector<int>> zigzagLevelOrder(TreeNode* root) 
{
	vector<vector<int>> level_order;
	helper(root,level_order,1);
	return level_order;
}

int main() {
	TreeNode* rt = new TreeNode(1);
	rt->left = new TreeNode(2);
	rt->right = new TreeNode(3);
	rt->left->left = new TreeNode(4);
	rt->right->left = new TreeNode(6);
	rt->right->right = new TreeNode(7);

    vector<vector<int>> TVS = zigzagLevelOrder(rt);
	
	for (int i=0; i<TVS.size(); i++)
	{
		for (int j=0; j<TVS[i].size(); j++)
		{
			cout << TVS[i][j] << " ";
		}
		cout << endl;
	}
	
	return 0;
}
```

## LeetCode 104
```c++
#include<iostream>
#include<queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 };
 
/*Recursive Method
int maxDepth(TreeNode* root) 
{
	if (root == NULL) return 0;
	return 1+max(maxDepth(root->left), maxDepth(root->right));
}
*/

//Iterative Method
int maxDepth(TreeNode* root)
{
	queue<TreeNode*> q;
	int layers = 0;
	if (root == NULL) return 0;
	q.push(root);
	
	while (!(q.empty())) 
	{
		int sz = q.size();
		for (int i=0; i<sz; i++)
		{
			TreeNode* currNode = q.front();
			q.pop();
			
			if (currNode->left != NULL) 
			{
				q.push(currNode->left);
			}
			if (currNode->right != NULL) 
			{
				q.push(currNode->right);
			}
		}
		layers++;
	}
	return layers;
}
int main() 
{
	TreeNode* root = new TreeNode(3);
	root->left = new TreeNode(9);
	root->right = new TreeNode(20);
	root->right->left = new TreeNode(15);
	root->right->right = new TreeNode(7);

	
	cout << maxDepth(root) << endl;
}
```

## LeetCode 105
```c++
#include<iostream>
#include<queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 };



TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
	if (preorder.empty())
	{
		return NULL;
	}
	int start = 0;
	int end = preorder.size();
	TreeNode* root = helper(preorder, inorder, start, end);
}

TreeNode* helper(vector<int>& preorder, vector<int>& inorder, int inStart int inEnd)
{
	static int inPre = 0;	
	int index = search(inorder, preorder[inPre]);
	inPre++;
	
	
	
	subroot->left = helper(preorder, inorder, inStart, index-1);
	subroot->right = helper(preorder, inorder, index+1, inEnd);
	
}



int main()
{
    int in[] = {1,2,3,489866,5};  
    char pre[] = { 'A', 'B', 'D', 'E', 'C', 'F' };  
    int len = sizeof(in);  
	cout << len << endl;
}
```

## LeetCode 965
```c++
#include <iostream>
#include <vector>

using namespace std;

struct TreeNode {
      int val;
      TreeNode *left;
      TreeNode *right;
      TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
//Usually helper functions are void function. 
void helper(TreeNode* subroot, int value, bool& judge) {
	if (subroot == NULL) return;
	if (subroot->val != value) judge = false;
	helper(subroot->left, value, judge);
	helper(subroot->right, value, judge);
}
 
bool isUnivalTree(TreeNode* root) {
	if (root == NULL) return true;
    int value = root->val;
	bool isUT = true;
	helper(root, value , isUT);
	return isUT;
}


int main() {
	TreeNode* first = new TreeNode(2);
	TreeNode* second = new TreeNode(3);
	TreeNode* third = new TreeNode(2);
	TreeNode* fourth = new TreeNode(2);
	TreeNode* fifth = new TreeNode(2);
	TreeNode* null = NULL;
	first->left = second;
	first->right = third;
	second->left = fourth;
	second->right = fifth;
	cout << isUnivalTree(null) << endl;
	return 0;
}
```

### Did you find this page helpful? Consider sharing it 🙌

