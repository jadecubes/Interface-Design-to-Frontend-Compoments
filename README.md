# Interface Design to Frontend Components
## Why
It's a common scinario that a front-end developer need to design user interface components based design on Figma. However, complicated interface can confuse developers from observing data dependencies. So, I suggest that 3 key principles can be applied when a fronend developer needs to plan his implementation.

## What Are the 3 Principles
[Frontend component changes depend on data changes.](https://dev.to/basal/data-oriented-frontend-development-1mk3) So it's crucial for frontend developers to correctly and clearly identify which data driving component display changes on user interface. The 3 principles are designed to help frontend developers to better find correct data dependencies.
1. List unit components
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


## Introduction to Implementation of React Provider
✅ React maintains an internal structure (linked list or Map) to track context consumers.

✅ When a context value changes, React directly notifies the subscribed consumers (O(1) lookup).

✅ Efficient propagation ensures that only necessary components re-render.

✅ This design avoids full tree traversal and unnecessary updates.

🎯 Bottom Line: React achieves O(1) context updates by maintaining a direct mapping between providers and consumers. 🚀

### Example
Context Provider Stores a Reference to Consumers
```typescript
const MyContext = createContext("default");

const ProviderComponent = () => {
  const [value, setValue] = useState("Hello");

  return (
    <MyContext.Provider value={value}>
      <ChildComponent />
    </MyContext.Provider>
  );
};

const ChildComponent = () => {
  const contextValue = useContext(MyContext);
  return <p>{contextValue}</p>;
};

```

When ChildComponent calls useContext(MyContext), React links it to MyContext.Provider.
The Provider maintains a list of subscribed consumers.

```
contextRegistry.set(MyContext, {
  value: "Hello",
  consumers: [ChildComponent],
});

```
Context Map to track consumers, so direct lookup for consumers: O(1). From above explanation, the use of Contxt leads to extra memory consumptions, so only use Context when it's required.

## Let's Practice with a Sample Requirement
[Demo](./requirementdemo.gif)

Create a dialog containing a table where the simple products, variation products and parent products display. User can select all products, some variation products in the table, or directly select parent products. The table needs to update selection information on the table parent product level and around the table.

The relationship among simple products, variation products and parent products is listed below,
- A variation product (or parent-child listing) is a product that has multiple variations, such as size, color, or material.
- A simple product is a product that does not have variations
- A product is the product containing variation products


## Apply 3 principles to Sample Requirement
1. List unit components
As the initial step, briefly separate the user interface to be 




