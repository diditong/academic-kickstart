---
title: Jiashuo's Programming Exercise
date: 2019-10-15
math: true
diagram: true
markup: mmark
image:
  placement: 3
  caption: 'Image credit: [**John Moeses Bauan**](https://unsplash.com/photos/OGZtQF8iC0g)'
---

### This is a documentation for my implementations of algorithms I learned from classes

## 1. Karatsuba Multiplication

```python
def KaraMult(x,y):
    if len(str(x)) == 1 or len(str(y)) == 1:
        return x*y
    
    else:
        n = max(len(str(x)),len(str(y)))
        n2 = n // 2
            
        a = x // 10**(n2)
        b = x % 10**(n2)
        c = y // 10**(n2)
        d = y % 10**(n2)
        
        ac = KaraMult(a,c)
        bd = KaraMult(b,d)
        ad_plus_bc = KaraMult(a+b,c+d) - ac - bd
        
        prod = ac * 10**(2*n2) + (ad_plus_bc * 10**n2) + bd

        return prod
```

## 2. Merge Sort

```python
def mergesort(alist):
    if (len(alist)>1):
        mid = len(alist)//2
        lefthalf = alist[:mid]
        righthalf = alist[mid:]
        mergesort(lefthalf)
        mergesort(righthalf)
        
        i,j,k=0,0,0
        while (i<len(lefthalf) and j<len(righthalf)):
            if (lefthalf[i]<righthalf[j]):
                alist[k]=lefthalf[i]
                i+=1
            else:
                alist[k]=righthalf[j]
                j+=1
            k+=1
        while(i<len(lefthalf)):
            alist[k]=lefthalf[i]
            i+=1
            k+=1
        while(j<len(righthalf)):
            alist[k]=righthalf[j]
            j+=1
            k+=1
```

## 3. Merge Sort (returns sorted list)

```python
def mergesort(alist):
    if (len(alist)>1):
        mid = len(alist)//2
        lefthalf = alist[:mid]
        righthalf = alist[mid:]
        mergesort(lefthalf)
        mergesort(righthalf)
        
        i,j,k=0,0,0
        while (i<len(lefthalf) and j<len(righthalf)):
            if (lefthalf[i]<righthalf[j]):
                alist[k]=lefthalf[i]
                i+=1
            else:
                alist[k]=righthalf[j]
                j+=1
            k+=1
        while(i<len(lefthalf)):
            alist[k]=lefthalf[i]
            i+=1
            k+=1
        while(j<len(righthalf)):
            alist[k]=righthalf[j]
            j+=1
            k+=1
```
## 4. Quick Sort (with the last element as the pivot)

```python

{% highlight python %}
import numpy as np
def swap(array,m,n):
    a = array[m]
    array[m] = array[n]
    array[n] = a

def quickSort(array,l,r):
    if (l<r):
        swap(array,r,l)  #always set the final element as the pivot
        p = partition(array,l,r)
        quickSort(array,l,p-1)
        quickSort(array,p+1,r)

def partition(array,l,r):
    pivot = array[l]
    #stat.median([array[l],array[(l+r)//2],array[r]])
    i = l+1
    for j in range(l+1,r+1):
        if (array[j] < pivot):
            swap(array,i,j)
            i+=1
    swap(array,i-1,l)
    return i-1

```

## 5. Count Inversions (with mergeSort() subroutine)

```python
def mergeSort(alist):
    right = len(alist)
    mid = right//2
    if (right == 1):
        return alist
    if (0 < mid):      
        lefthalf = mergeSort(alist[:mid])
    if (mid < right):  
        righthalf = mergeSort(alist[mid:])

    i=0
    j=0
    sortedlist = []
        
    while(i<mid and j<right-mid):
        if(lefthalf[i]<=righthalf[j]):
            sortedlist.append(lefthalf[i])
            i+=1
        else:
            sortedlist.append(righthalf[j])
            j+=1
            
    while(i<mid):
        sortedlist.append(lefthalf[i])
        i+=1
    while(j<right-mid):
        sortedlist.append(righthalf[j])
        j+=1
    return sortedlist
	
def countInversions(array):
    if (len(array)==1):
        return 0
    mid = len(array)//2
    num_invs_left = countInversions(array[:mid])
    num_invs_right = countInversions(array[mid:])
    
    lefthalf = mergeSort(array[:mid])
    righthalf = mergeSort(array[mid:])
    i=j=0
    num_invs_between = 0
    while (j<len(righthalf) and i<len(lefthalf)):
        if (righthalf[j]>lefthalf[i]):
            i+=1
        else:
            num_invs_between+=len(lefthalf)-i
            j+=1
    
    return num_invs_left+num_invs_right+num_invs_between

```
## 6. RSelect (Random Select with partition subroutine)

```python
def swap(array,m,n):
    a = array[m]
    array[m] = array[n]
    array[n] = a

def partition(array,l,r):
    i_pivot = np.random.randint(r)
    swap(array,i_pivot,l)
    pivot = array[l]
    #stat.median([array[l],array[(l+r)//2],array[r]])
    i = l+1
    for j in range(l+1,r):
        if (array[j] < pivot):
            swap(array,i,j)
            i+=1
    swap(array,l,i-1)
    return i

def RSelect(A,i):
    length = len(A)
    if length == 1:
        return A[i]
    j = partition(A,0,length)
    if j+1 == i:
        return A[j]
    elif j+1 < i:
        return RSelect(A[j:],i-j)
    else:
        return RSelect(A[0:j],i)

for i in range(1000):
    kargerDict = backupDict.copy()
    for i in range(198):
        #Remove the chosen connection from the dictionary
        delete = list(kargerDict)[np.random.randint(len(kargerDict))]
        i1 = delete[0]
        i2 = delete[1]
        del kargerDict[delete]
        #Transfer the count from old connections to new connections
        for old_key in kargerDict.copy():
            x,y = old_key[0],old_key[1]
            if x == i2:
                m = i1
                n = y
            elif y == i2:
                m = i1
                n = x
            else:
                continue
            m,n = sorted([m,n])
            new_key = (m,n)
            if new_key in kargerDict.keys():
                kargerDict[new_key] += kargerDict[old_key]
            else:
                kargerDict[new_key] = kargerDict[old_key]
            del kargerDict[old_key]
    if mincut > list(kargerDict.values())[0]:
        mincut = list(kargerDict.values())[0]
    print("Cut for current iteration is: ", mincut)

```
## 7. Karger algorithm for counting minimum cut

```python
kargerDict = {}
#Read the text file into a dictionary
with open('kargerMinCut.txt', 'r') as f:
    i = 0
    while i < 200:
        line = f.readline()
        line = line.split('\t')
        line = line[:-1]
        
        idx = 0
        for string in line:
            line[idx] = int(string)
            idx += 1
        
        m = line[0]
        for j in range(1,len(line)):
            n = line[j]
            if n > m:
                kargerDict[(m,n)] = 1
        i += 1
    for i in range(1,201):
        for j in range(i+1,201):
            if (i,j) not in kargerDict.keys():
                kargerDict[(i,j)] = 0
    #Backup the dictionary for further processing
    backupDict = kargerDict
mincut = 10000

for i in range(1000):
    kargerDict = backupDict.copy()
    for i in range(198):
        #Remove the chosen connection from the dictionary
        delete = list(kargerDict)[np.random.randint(len(kargerDict))]
        i1 = delete[0]
        i2 = delete[1]
        del kargerDict[delete]
        #Transfer the count from old connections to new connections
        for old_key in kargerDict.copy():
            x,y = old_key[0],old_key[1]
            if x == i2:
                m = i1
                n = y
            elif y == i2:
                m = i1
                n = x
            else:
                continue
            m,n = sorted([m,n])
            new_key = (m,n)
            if new_key in kargerDict.keys():
                kargerDict[new_key] += kargerDict[old_key]
            else:
                kargerDict[new_key] = kargerDict[old_key]
            del kargerDict[old_key]
    if mincut > list(kargerDict.values())[0]:
        mincut = list(kargerDict.values())[0]
    print("Cut for current iteration is: ", mincut)

```

## 8. Dijkstra's Algorithm

```C++
#include <iostream>
#include <cstring>
#include <vector>
#include <fstream>
#include <limits>

using namespace std;

struct Edge
{
	int dest, weight;
};

struct AdjList
{
	int src;
	vector<Edge> list;
};

struct Node
{
	int idx;
	int dist;
	bool visited;
};

class Graph
{
public:
	vector<Node> nodes;
	vector<AdjList> graph;
	
	Graph(string filename);
	int getSize();
	vector<int> Dijkstra(int start, vector<int> ends);
	int setMinNode();
	bool existNonVisited();
};

vector<string> split(string& line, char delimiter)
{
	vector<string> v;
	string token;
	for (char const c: line)
	{
		if (c == delimiter)
		{
			v.push_back(token);
			token.clear();
		}
		else
		{
			token += c;
		}
	}
	v.push_back(token);
	return v;
}

Graph::Graph(string filename)
{
	string line;
	ifstream myfile(filename);
	
	if (myfile.is_open())
	{
		while ( getline(myfile,line) )
		{
			//Read a single line into edge and list
			vector<string> splt1 = split(line, ' ');
			splt1.pop_back();
			AdjList l;
			l.src = stoi(splt1[0]);
			
			for (int i=1; i<splt1.size(); i++)
			{
				vector<string> splt2 = split(splt1[i], ',');

				Edge e;		
				e.dest = stoi(splt2[0]);
				e.weight = stoi(splt2[1]);
				
				l.list.push_back(e);
			}
			
			graph.push_back(l);
			
		}
		
	myfile.close();
	
	}
}

int Graph::getSize()
{
	return graph.size();
}

int Graph::setMinNode()
{
	int min_idx = 0;
	for (int curr_idx=1; curr_idx<nodes.size(); curr_idx++)
	{	
		//cout << "From setMinNode: Node " << curr_idx << " is visited? " << nodes[curr_idx].visited << endl;
		//cout << "From setMinNode: Node " << curr_idx << " has a value " << nodes[curr_idx].dist << endl;
		if (!nodes[curr_idx].visited)
		{
			// << "curr_idx is " << curr_idx << ", dist is " << nodes[curr_idx].dist << endl;
			if (nodes[curr_idx].dist < nodes[min_idx].dist)
			{
				min_idx = curr_idx;
			}
		}
	}
	//cout << "Minimum Index is " << min_idx << endl;
	//cout << "returned min_idx is " << min_idx << endl; 
	return min_idx;
}

bool Graph::existNonVisited()
{
	for (int curr_idx=1; curr_idx<nodes.size(); curr_idx++)
	{
		if (nodes[curr_idx].visited == false)
		{
			return true;
		}
	}
	return false;
}

vector<int> Graph::Dijkstra(int start, vector<int> ends)
{
	//Mark initial node with a weight 0. Mark the rest nodes with infinity.
	Node firstNode = {
		0, numeric_limits<int>::max(), true
	};
	nodes.push_back(firstNode);
	//
	int sz = graph.size();
	Node n = {
		1, 0, false
	};
	nodes.push_back(n);

	for (int i=2; i<=sz ; i++)
	{
		Node n = {
			i, numeric_limits<int>::max(), false
		};
		nodes.push_back(n);
	}
	
	while (existNonVisited())
	{
		//Set the non-visited node with the minimum current distance as the current node C.
		int c_idx = setMinNode();
		//For each neighbor n, add c with c-n. If smaller than current weight of n, set it as 
		//new distance of n.
		for (Edge e : graph[c_idx-1].list)
		{
			//cout << "Size of the list is " << graph[c_idx-1].list.size() << endl;
			//cout << "dest " << e.dest << " is visited? " << nodes[e.dest].visited << endl;
			if (!nodes[e.dest].visited)
			{
				//cout << "node " << c_idx << " is compared to " << e.dest << endl;
				if (nodes[c_idx].dist + e.weight < nodes[e.dest].dist)
				{
					nodes[e.dest].dist = nodes[c_idx].dist + e.weight;
				}
			}
		}
		//set current node to be visited
		//cout << nodes[c_idx].idx << endl;
		nodes[c_idx].visited = true;
	}
	
	//Generate the final distance list for output
	vector<int> shortestDistances;
	for (int end : ends) 
	{
		shortestDistances.push_back(nodes[end].dist);
	}
	return shortestDistances;
	
}

int main() 
{
	Graph G = Graph("dijkstraData.txt");
	//cout << G.graph[0].list[0].weight << endl;
	vector<int> endpoints = {7,37,59,82,99,115,133,165,188,197};
	for (int distance : G.Dijkstra(1,endpoints))
	{
		cout << distance << " ";
	}
	cout << endl;
	return 0;
}
```

### Did you find this page helpful? Consider sharing it 🙌

