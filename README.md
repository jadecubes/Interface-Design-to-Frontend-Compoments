# Interface Design to Frontend Components
## Why
It's a common scinario that a front-end developer need to design user interface components based design on Figma. However, complicated interface can confuse developers from observing data dependencies. So, I suggest that 3 key principles can be applied when a fronend developer needs to plan his implementation.

## What Are the 3 Principles
1. Find unit components
2. Find data dependency: sometimes, data dependency is not obvious, we can figure that out by class diagrams.
3. Data sharing: if there are multiple layers of components that need to share the same data, React provider is the most suitable option. Howerver, in situations where only few props need to be shared with a few components, applying data to props and using props for data passing is enough.

```
Facts about React Fiber Tree
1. Fiber Linked Nodes
- Each Fiber points to its parent, child, and sibling nodes.
- When looking up context, React walks the linked list upwards until it finds a Provider.

2.  Fiber Tree Component Hierarchy
- Each component is a Fiber Node.
- A Provider is a special Fiber Node that holds a context value.
- The Consumer traverses up the tree to find the nearest Provider

```


```
With a React context, how does the context update components that uses data in the outside context?
The update includes 2 phases,


```

## Let's Take a Requirement as an Example




