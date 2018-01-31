# RTree
C# RTree implementation

[![Build status](https://ci.appveyor.com/api/projects/status/j2avp93pimks10do?svg=true)](https://ci.appveyor.com/project/marchello2000/rtree)

Forked from [https://github.com/enyim/RTree](https://github.com/enyim/RTree) to fix bugs and add a nuget package  
C# port based on [this](https://github.com/mourner/rbush) JavaScript implementation by [Vladimir Agafonkin](http://agafonkin.com/).

RTree is a very fast spatial data structure and index.

## Usage
```cs
using Enyim.Collections;

RTree<Line> rtree = new RTree<Line>();

// Bulk insertion (2-3x faster than 1 by 1 insertion)
List<RTreeNode<Line>> nodes = new List<RTreeNode<Line>>();
Line l = new Line(0, 0, 10, 10);
nodes.Add(new RTreeNode<Line>(
    l, 
    new Envelope((int)Math.Min(l.X1, l.X2), (int)Math.Min(l.Y1, l.Y2), (int)Math.Max(l.X1, l.X2), (int)Math.Max(l.Y1, l.Y2))
    ));

rtree.Load(nodes);

// One-off insertion
rtree.Insert(l, new Envelope(...));

// Search
var results = rtree.Search(new Envelope(0, 0, 1, 1));

foreach (var result in results)
{
    Line l = result.Data;
    ...
}
```