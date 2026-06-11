# Class

## JavaScript

```
class Node {
  constructor(val = 0, prev = null, next = null) {
    this.val = val;
    this.prev = prev;
    this.next = next;
  }
}

const n1 = new Node(1)
const n2 = new Node(2, n1)
const n3 = new Node(3, n2, n1)
n1.prev = n3;
n1.next = n2;
n2.next = n3;


function detectCycle(n) {
  let fast = n, slow = n;
  while (fast && fast.next) {
    console.log('fast: ' + fast.val + ', slow: ' + slow.val);
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true;
    }
  }
  return false;
}

console.log('detectCycle(n1): ', detectCycle(n1));
```

## TypeScript

```
// Note: Node may have conflicts with the global Node type provided by the DOM typings.
class Node {
  val : number;
  prev : Node | null;
  next : Node | null;

  constructor(val = 0, prev : Node|null = null, next: Node|null = null) {
    this.val = val;
    this.prev = prev;
    this.next = next;
  }
}

const n1 = new Node(1)
const n2 = new Node(2, n1)
const n3 = new Node(3, n2, n1)
n1.prev = n3;
n1.next = n2;
n2.next = n3;


function detectCycle(n : Node) {
  let fast:Node | null = n, slow : Node | null = n;
  while (slow && fast && fast.next) {
    // console.log('fast: ' + fast.val + ', slow: ' + slow.val);
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true;
    }
  }
  return false;
}

console.log('detectCycle(n1): ', detectCycle(n1));
```
