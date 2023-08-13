# Kruskal_find_min_Spanning_tree_py


````Py

class DSU:
    def __init__(self, n):
        self.n = n
        self.par  = [x for x in range(n)] #parent array

    def find(self, x):
        # recursive find of the parent of each node and end when index and value same
        if self.par[x] != x:
            return self.find(self.par[x]) # now pass the parent of x in the argument
        return x
    def union(self, x, y):
        g1 = self.find(x)
        g2 = self.find(y)
        if g1 == g2:
            #cycle
            return False
        if g1 > g2: # set parent in asc
            g1, g2 = g2, g1
        self.par[g2] = g1  # now g1 is parent of g2; now g1 is smaller than g2 (sorting)
        return True

def kruskal(n, edges):
    dsu = DSU(n)
    edges.sort(key = lambda edge: edge[2])
    msg_weight = 0
    for src, dest, w in edges:
        if dsu.union(src, dest): # get the sorted, parent child node, and find the weight to make union
            msg_weight += w 
    return msg_weight

edges = [[0,1,4],[1,2,8], [2, 3, 7], [3, 4, 9], [4,5,10], [3,5,14],
         [2,5, 4],[5,6,2],[8,6,6],[2,8,2],[7,6,1],[7,8,7],[1, 7, 11],[0,7,8]]
n  = 9
result = kruskal(n, edges)
print(result)


````
