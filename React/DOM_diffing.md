# React DOM diffing

**React DOM diffing**, also known as the **diffing algorithm**, is a core mechanism in React's **reconciliation** process
that enables efficient updates to the actual browser DOM. When a component's state or props change, React creates a 
new Virtual DOM tree representing the updated UI. The diffing algorithm then compares this new Virtual DOM tree with the 
previous one to identify the minimal set of changes required.

Here's how it works:

- Virtual DOM Comparison:
  React compares the new Virtual DOM tree with the old one, node by node, using a set of heuristics.
- Identifying Differences:
  - Element Type: If two elements at the same position have different types (e.g., a <div> becomes a <span>), React will tear down the old component and rebuild the new one from scratch.
  - Props: If the element types are the same, React compares their props. Only the changed props are updated on the corresponding actual DOM element.
  - Children (Key-Based Reconciliation): For lists of children, React uses the key prop to identify stable elements across renders. This allows React to efficiently update, add, or remove items in a list without re-rendering the entire list. Without keys, React might re-render all elements if the order or number of items changes. 
- Minimal DOM Updates:
    Based on the identified differences, React calculates the most efficient way to update the actual browser DOM. It only applies the necessary changes, minimizing direct DOM manipulations, which are typically expensive operations. 

This process significantly improves performance by avoiding unnecessary re-renders of the entire UI and ensuring that only the parts of the DOM that require changes are updated. 

## References

- https://refine.dev/blog/react-virtual-dom/#introduction
