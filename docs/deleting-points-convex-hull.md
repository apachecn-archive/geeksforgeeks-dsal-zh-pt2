# 从凸包中删除点

> 原文:[https://www.geeksforgeeks.org/deleting-points-convex-hull/](https://www.geeksforgeeks.org/deleting-points-convex-hull/)

给定一组固定的点。我们需要找到给定集合的凸包。当从集合中移除一个点时，我们还需要找到凸包。

示例:

```
Initial Set of Points: (-2, 8) (-1, 2) (0, 1) (1, 0)
                        (-3, 0) (-1, -9) (2, -6) (3, 0) 
                        (5, 3) (2, 5) 
Initial convex hull:- (-2, 8) (-3, 0) (-1, -9) (2, -6)
                      (5, 3)
Point to remove from the set : (-2, 8)
Final convex hull: (2, 5) (-3, 0) (-1, -9) (2, -6) (5, 3)
```

先决条件:[凸包(简单分治算法)](https://www.geeksforgeeks.org/convex-hull-simple-divide-conquer-algorithm/)
解决上述问题的算法非常容易。我们只需检查要移除的点是否是凸包的一部分。如果是，那么我们必须从初始集合中移除该点，然后再次制作凸包(参考[凸包(分治)](https://www.geeksforgeeks.org/convex-hull-simple-divide-conquer-algorithm/))。

如果没有，那么我们已经有了解(凸包不会改变)。

## C++

```
// C++ program to demonstrate delete operation
// on Convex Hull.
#include<bits/stdc++.h>
using namespace std;

// stores the center of polygon (It is made
// global because it is used in comare function)
pair<int, int> mid;

// determines the quadrant of a point
// (used in compare())
int quad(pair<int, int> p)
{
    if (p.first >= 0 && p.second >= 0)
        return 1;
    if (p.first <= 0 && p.second >= 0)
        return 2;
    if (p.first <= 0 && p.second <= 0)
        return 3;
    return 4;
}

// Checks whether the line is crossing the polygon
int orientation(pair<int, int> a, pair<int, int> b,
                pair<int, int> c)
{
    int res = (b.second-a.second)*(c.first-b.first) -
              (c.second-b.second)*(b.first-a.first);

    if (res == 0)
        return 0;
    if (res > 0)
        return 1;
    return -1;
}

// compare function for sorting
bool compare(pair<int, int> p1, pair<int, int> q1)
{
    pair<int, int> p = make_pair(p1.first - mid.first,
                                 p1.second - mid.second);
    pair<int, int> q = make_pair(q1.first - mid.first,
                                 q1.second - mid.second);

    int one = quad(p);
    int two = quad(q);

    if (one != two)
        return (one < two);
    return (p.second*q.first < q.second*p.first);
}

// Finds upper tangent of two polygons 'a' and 'b'
// represented as two vectors.
vector<pair<int, int> > merger(vector<pair<int, int> > a,
                               vector<pair<int, int> > b)
{
    // n1 -> number of points in polygon a
    // n2 -> number of points in polygon b
    int n1 = a.size(), n2 = b.size();

    int ia = 0, ib = 0;
    for (int i=1; i<n1; i++)
        if (a[i].first > a[ia].first)
            ia = i;

    // ib -> leftmost point of b
    for (int i=1; i<n2; i++)
        if (b[i].first < b[ib].first)
            ib=i;

    // finding the upper tangent
    int inda = ia, indb = ib;
    bool done = 0;
    while (!done)
    {
        done = 1;
        while (orientation(b[indb], a[inda], a[(inda+1)%n1]) >=0)
            inda = (inda + 1) % n1;

        while (orientation(a[inda], b[indb], b[(n2+indb-1)%n2]) <=0)
        {
            indb = (n2+indb-1)%n2;
            done = 0;
        }
    }

    int uppera = inda, upperb = indb;
    inda = ia, indb=ib;
    done = 0;
    int g = 0;
    while (!done)//finding the lower tangent
    {
        done = 1;
        while (orientation(a[inda], b[indb], b[(indb+1)%n2])>=0)
            indb=(indb+1)%n2;

        while (orientation(b[indb], a[inda], a[(n1+inda-1)%n1])<=0)
        {
            inda=(n1+inda-1)%n1;
            done=0;
        }
    }

    int lowera = inda, lowerb = indb;
    vector<pair<int, int> > ret;

    //ret contains the convex hull after merging the two convex hulls
    //with the points sorted in anti-clockwise order
    int ind = uppera;
    ret.push_back(a[uppera]);
    while (ind != lowera)
    {
        ind = (ind+1)%n1;
        ret.push_back(a[ind]);
    }

    ind = lowerb;
    ret.push_back(b[lowerb]);
    while (ind != upperb)
    {
        ind = (ind+1)%n2;
        ret.push_back(b[ind]);
    }
    return ret;

}

// Brute force algorithm to find convex hull for a set
// of less than 6 points
vector<pair<int, int> > bruteHull(vector<pair<int, int> > a)
{
    // Take any pair of points from the set and check
    // whether it is the edge of the convex hull or not.
    // if all the remaining points are on the same side
    // of the line then the line is the edge of convex
    // hull otherwise not
    set<pair<int, int> >s;

    for (int i=0; i<a.size(); i++)
    {
        for (int j=i+1; j<a.size(); j++)
        {
            int x1 = a[i].first, x2 = a[j].first;
            int y1 = a[i].second, y2 = a[j].second;

            int a1 = y1-y2;
            int b1 = x2-x1;
            int c1 = x1*y2-y1*x2;
            int pos = 0, neg = 0;
            for (int k=0; k<a.size(); k++)
            {
                if (a1*a[k].first+b1*a[k].second+c1 <= 0)
                    neg++;
                if (a1*a[k].first+b1*a[k].second+c1 >= 0)
                    pos++;
            }
            if (pos == a.size() || neg == a.size())
            {
                s.insert(a[i]);
                s.insert(a[j]);
            }
        }
    }

    vector<pair<int, int> >ret;
    for (auto e : s)
        ret.push_back(e);

    // Sorting the points in the anti-clockwise order
    mid = {0, 0};
    int n = ret.size();
    for (int i=0; i<n; i++)
    {
        mid.first += ret[i].first;
        mid.second += ret[i].second;
        ret[i].first *= n;
        ret[i].second *= n;
    }
    sort(ret.begin(), ret.end(), compare);
    for (int i=0; i<n; i++)
        ret[i] = make_pair(ret[i].first/n, ret[i].second/n);

    return ret;
}

// Returns the convex hull for the given set of points
vector<pair<int, int>> findHull(vector<pair<int, int>> a)
{
    // If the number of points is less than 6 then the
    // function uses the brute algorithm to find the
    // convex hull
    if (a.size() <= 5)
        return bruteHull(a);

    // left contains the left half points
    // right contains the right half points
    vector<pair<int, int>>left, right;
    for (int i=0; i<a.size()/2; i++)
        left.push_back(a[i]);
    for (int i=a.size()/2; i<a.size(); i++)
        right.push_back(a[i]);

    // convex hull for the left and right sets
    vector<pair<int, int>>left_hull = findHull(left);
    vector<pair<int, int>>right_hull = findHull(right);

    // merging the convex hulls
    return merger(left_hull, right_hull);
}

// Returns the convex hull for the given set of points after
// remviubg a point p.
vector<pair<int, int>> removePoint(vector<pair<int, int>> a,
                                   vector<pair<int, int>> hull,
                                   pair<int, int> p)
{
    // checking whether the point is a part of the
    // convex hull or not.
    bool found = 0;
    for (int i=0; i < hull.size() && !found; i++)
        if (hull[i].first == p.first &&
                hull[i].second == p.second)
            found = 1;

    // If point is not part of convex hull
    if (found == 0)
        return hull;

    // if it is the part of the convex hull then
    // we remove the point and again make the convex hull
    // and if not, we print the same convex hull.
    for (int i=0; i<a.size(); i++)
    {
        if (a[i].first==p.first && a[i].second==p.second)
        {
            a.erase(a.begin()+i);
            break;
        }
    }

    sort(a.begin(), a.end());
    return findHull(a);
}

// Driver code
int main()
{
    vector<pair<int, int> > a;
    a.push_back(make_pair(0, 0));
    a.push_back(make_pair(1, -4));
    a.push_back(make_pair(-1, -5));
    a.push_back(make_pair(-5, -3));
    a.push_back(make_pair(-3, -1));
    a.push_back(make_pair(-1, -3));
    a.push_back(make_pair(-2, -2));
    a.push_back(make_pair(-1, -1));
    a.push_back(make_pair(-2, -1));
    a.push_back(make_pair(-1, 1));

    int n = a.size();

    // sorting the set of points according
    // to the x-coordinate
    sort(a.begin(), a.end());
    vector<pair<int, int> >hull = findHull(a);

    cout << "Convex hull:\n";
    for (auto e : hull)
        cout << e.first << " "
             << e.second << endl;

    pair<int, int> p = make_pair(-5, -3);
    removePoint(a, hull, p);

    cout << "\nModified Convex Hull:\n";
    for (auto e:hull)
        cout << e.first << " "
             << e.second << endl;

    return 0;
}
```

输出:

```
convex hull:
-3 0
-1 -9
2 -6
5 3
2 5
```

**时间复杂度:**
很容易看出，每个查询花费的最大时间是构造凸包所花费的时间，它是 O(n*logn)。所以，整体复杂度是 O(q*n*logn)，其中 q 是要删除的点数。

本文由[阿姆利则瓦格米](https://www.facebook.com/amritya.vagmi)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。