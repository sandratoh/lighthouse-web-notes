# Trees

## What are Trees?

A data structure that helps organize information

## What are Trees Made Of?

- **Node** - each circle in the tree
- **Edges** - the connection between the nodes

## Different Nodes

- **Root node** - node at the top of the tree
- **Leaf nodes** - nodes at the very bottom
- **Parent node** - node that encompasses other node(s) below it
  - Every node except root has a single parent node
- **Children nodes** - nodes that are directly below a parent node
- **Sibling nodes** - all children with the same parent node

## Tree Traversal

### Breadth First Traversal (Level-Order)

- Start with the root node
- The move onto the root's children
- Then move onto those node's children

> **Bread first traversal** will always visit the nodes closest to the root node before moving on to the nodes that are farthest away.

### Depth First Traversal

- Start with the root node
- Visit each node on an entire path, all the way to the leaf node(s)
- Go to the next path

#### Types of Depth First Traversal

- **Preorder** - <root> --> <left> --> <right>

- **Inorder** - <left> --> <root> --> <right>

- **Postorder** - <left> --> <right> --> <root>

## Recursion and Tree Traversal

> Trees are recursive because each node is in fact the root node of its own tree

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.parent = null;
    this.children = [];
  }
  depthFirstTraversal() {
    // Visit current node
    console.log(this);

    // Loop through every child of current node, repeating first step
    for (const childNode of this.children) {
      childNode.depthFirstTraversal();
    }
  }
}
```
