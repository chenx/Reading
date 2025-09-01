# Reflow and Repaint (回流与重绘)

Reflow and Repaint are two distinct but often related processes in a web browser's rendering engine that affect how a webpage is displayed and updated.

## 1. Reflow (or Layout)

### Definition:

Reflow is the process where the browser recalculates the layout and position of elements on a webpage. This involves determining the size and position of every visible element in the Document Object Model (DOM) and constructing the render tree.

### Triggers:

Reflow is triggered by any change that affects the geometry or position of elements, which can then cascade to other elements. Examples include:

- Adding, removing, or updating DOM nodes.
- Changing CSS properties that affect layout, such as width, height, margin, padding, font-size, display, or position.
- Resizing the browser window.
- Activating pseudo-classes like :hover that change layout-affecting properties. 
    
### Performance Impact:

Reflow is computationally expensive because it requires recalculating the layout of potentially a large portion of the page, or even the entire page. 

## 2. Repaint

### Definition:

Repaint is the process where the browser re-draws the visual appearance of elements on the screen. This involves painting pixels to reflect changes in visual properties.

### Triggers:

Repaint is triggered by changes to an element's visual properties that do not affect its layout or position. Examples include:
- Changing CSS properties like color, background-color, visibility (when visibility: hidden is used, as it doesn't remove the element from the layout flow), box-shadow, or text-decoration.
- Changing image sources. 

### Performance Impact:

Repaint is generally less computationally expensive than reflow because it only involves updating the visual representation of elements without recalculating their layout. 

## 3. Relationship

A reflow almost always leads to a repaint, as recalculating the layout necessitates re-drawing the affected elements.

A repaint does not necessarily lead to a reflow.

## 4. Optimization

Minimizing unnecessary reflows and repaints is crucial for web performance. Strategies include:

#### Batching DOM changes:

Grouping multiple DOM manipulations together to trigger a single reflow/repaint.

#### Using CSS transforms and opacity for animations:

These properties are often hardware-accelerated and can be animated without triggering reflows.

#### Avoiding layout thrashing:

Reading and writing to the DOM in separate operations to prevent forced synchronous layout calculations.

#### Using CSS classes for style changes:

Applying or removing CSS classes is often more efficient than directly manipulating inline styles.

## 5. References

-  [Understanding Reflow and Repaint in the browser](https://dev.to/gopal1996/understanding-reflow-and-repaint-in-the-browser-1jbg)
-  [What are Reflow and Repaint? How to optimize?](https://www.explainthis.io/en/swe/repaint-and-reflow)

### Appendix 1: Browser Rendering Process

#### 1. Parsing HTML and Style Calculation:

Parses HTML into DOM, parses CSS into CSSOM, and merges DOM and CSSOM into render tree.

  - DOM - Document Object Model
  - CSSOM - CSS Object Model

#### 2. Layout

  - browser also needs to calculate the size and position of each node on the screen. This process is called layout and produces a layout tree.

#### 3. Painting

#### 4. Compositing

  - Compositing is a technique of dividing the page into layers (layers), and this technique will be executed on a separate thread called compositor thread.
  - After this process is completed, a layer tree will be generated, and finally rendered to the screen.
