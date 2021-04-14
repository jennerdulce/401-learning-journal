# Binary Tree, Binary Search Trees, Recursion, and Career Tips

## Recursion

- Solve a problem with a diminishing data set
- Traverse data structure and at some point, do some work
- Base Case
- You can choose to write with a helper function

```javascript
function add(a, b){
  if (b == 0) {return a}
  
  return add(a + 1, b - 1)
}

preOrder(node, nodes=[]) {
  nodes.push(node.value);
  if(node.left) {this.preOrder(node.left, nodes);}
  if(node.right) {this.preOrder(node.right, nodes);}
  return nodes;
}
```

## Binary Trees - Refer to Code Challenge/BST

### Parts

- Root: beginning of a tree
- Edges/branches: connect nodes
- Leaf: node with no connecting nodes
- Subtree: a node with 2 connecting nodes below the root can be considered a sub tree.
  - the root of this subtree would refer to the node that has 2 children
  - any node can be the `root` of the next tree
- Height: max # of edges
- Width: widest set across
- Balanced: Difference in height Left to right < 1
- Moving through the tree is known as: `visit`, `evaluate`, `land on`

### Node Parts

- Left: connects a node to the left
- Right: connects a node to the right

## Binary Search Trees

- Difference between Binary Trees and Binary Search Trees is that Binary Search Trees have a rule when adding new nodes to the tree
  - if the new node is > than the root node.. connect to the right
  - if the new node is < than the root node.. connect to the left
- Similar like to a binary Search, the Binary Search Tree's Big O Time is: O(log n)
  - the algorith cuts the search in half until search is found or nothing is found
  - Length of time to search a number out of one billion takes roughly 18 interations of the search

```javascript
class BinaryTree {
  constructor() {
    this.root = null;
  }

  preOrder(node, nodes=[]) {
    nodes.push(node.value);
    if(node.left) {this.preOrder(node.left, nodes);}
    if(node.right) {this.preOrder(node.right, nodes);}
    return nodes;
  }

  inOrder(node, nodes=[]) {
    if(node.left) {this.inOrder(node.left, nodes);}
    nodes.push(node.value);
    if(node.right) {this.inOrder(node.right, nodes);}
    return nodes;
  }

  postOrder(node, nodes=[]) {
    if(node.left) {this.postOrder(node.left, nodes);}
    if(node.right) {this.postOrder(node.right, nodes);}
    nodes.push(node.value);
    return nodes;
  }
}

class BinarySearchTree extends BinaryTree {
  add(value, current = this.root) {
    const newNode = new Node(value);
    if (!this.root) {
      this.root = newNode;
    }
    if (!current) {
      return newNode;
    }
    // traverse Right
    if (newNode.value > current.value) {
      current.right = this.add(value, current.right);
    } else { // traverse Left
      current.left = this.add(value, current.left);
    }
    return current;
  }

  contains(value) {
    // O(n)
    // let nodes = this.preOrder(this.root);
    // if (nodes.includes(value)){
    //   return true;
    // } else {
    //   return false;
    // }
    let current = this.root;
    while(current){
      if (value === current.value){
        return true;
      }
      if(value > current.value){
        current = current.right;
      } else {
        current = current.left;
      }
    }
    return false;
  }
}
```

## Career Tips

### Offer and Negotiations

- Even as a Junior Developer, a salary can be negotiated 5-10% to match financial needs if necessary
- Choose to get paid upfront signup bonus to pay off some things and reduce salary pay
- Think about covering your personal needs
- It is okay to pass the first offer
- Gameplan for counter offer
  - be prepared to negotiate a work life balance (remote days and vacation etc)
- Be aware of industry standard for salary and benefits (compensation and health care)

### Targeted Job Search

- Narrow job search to position and specific greater region
- Local job offers
- Indeed, LinkedIn, Glassdoor
  - find job on glass door
  - research on Indeed
  - LinkedIn is a fantastic way to job search
- Try being specific and also general
- Aim high, be realistic
- Track you interactions with the companies and your progress toward them
- Utilize interview section at Indeed
- Set up LinkedIn and indeed search to email you about job positions
- Work on quizzes on LinkedIn

### Networking

- Find ways to connect to other people from friends and connections from linked in
- Create Circle; Company based in Seattle that offer you part time jobs based on your skillset
- Art of small talk. Practice it, it is a skill that can be obtained with practice!
Stay Relevant. Get in and stay in peoples heads
- Have multiple pitches that vary in length and altered based on who you're talking to (casual, professional)
- Get in people' minds and stay in there
- Return the faor to those that want to connect