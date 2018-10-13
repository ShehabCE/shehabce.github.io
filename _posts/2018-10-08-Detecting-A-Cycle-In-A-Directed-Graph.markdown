---
layout: post
title:  "Detecting A Cycle In A Directed Graph [Course Schedule]"
date:   2018-03-18 08:40:00
<!-- author: Shehab -->
categories: Technical
tags: Algorithms
cover:  "/assets/posts/ides-do-hurt.png"
---

{% highlight c++ %}
class Graph {
private:
    list<int> *adj;
    int vertices;
public:
    bool isThereACycle(int v, bool *recStack, bool *visited)
    {
        if(!visited[v])
        {
            visited[v] = true;
            recStack[v] = true;
            for(auto it = adj[v].begin(); it != adj[v].end(); it++)
            {
                if(!visited[*it] && isThereACycle(*it, recStack, visited))
                    return true;
                else if(recStack[*it])
                    return true;
            }
        }
        recStack[v] = false;
        return false;
    }
    bool canFinish(int numCourses, vector< pair < int, int > >& prerequisites) {
        vertices = numCourses;
        adj = new list <int> [vertices];
        for(int i=0; i < prerequisites.size(); i++) {
            int u = prerequisites[i].first;
            int v = prerequisites[i].second;
            adj[u].push_back(v);
        }
        
        bool *recStack = new bool[vertices] {false};
        bool *visited = new bool[vertices] {false};
        
        for(int i=0; i<vertices; i++)
            if(isThereACycle(i, recStack, visited))
                return false;

        return true;
    }
};

{% endhighlight %}

