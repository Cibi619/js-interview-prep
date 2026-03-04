1. What is specificity?
- CSS Specificity is a set of rules that browsers use to determine which CSS style should be applied to an element when there are multiple conflicting styles targeting the same element.
- Inline Styles - 1 0 0 0 
- IDs           - 0 1 0 0
- Classes,attributes,pseudoclasses  - 0 0 1 0
- Elements, pseudo-elements - 0 0 0 1

2. Would you ever unit test CSS?
- I would say no, as CSS is more about producing a desired visual outcome, rather than logics which usually are unit tested.

3. What are some concerns to keep in mind with web accessibility in HTML and CSS?
- Web accessibility ensures that websites are used by everyone. 
- Some points to keep in mind:
    - Using Semantic tags
    - Heading hierarchy
    - Focus states should be visible
    - Color contrast (can be checked by chrome DevTools)
    - Font sizes, line heights and spaces
    - alt text for images

4. What is your general workflow when adapting a Figma design for use in a website?
- First, analyze and plan. Look at the design, color palette, typography, spacing system used, breakpoints, etc.
- Clarify with designers - ask qns such as what's the mobile/tablet behavior (if not provided), ask about error states.
- Setup CSS/SCSS variables
- Setup Mixins
- Handle responsive design

5. What are mixins?
- Mixins allow us to group multiple CSS declarations in a single name that can be included in other selectors.
    ```
    @mixin transform {
        -moz-transform: rotate(180deg);
        transform: rotate(180deg);
    }
    p {
        font-size: 1em;
        @include transform
    }
    ```
- We can use it like this inside with any selector.

6. When would you use :has() or :not() in your selectors?
- :has() and :not() are CSS pseudoclasses that can be used to write more efficient and maintainable CSS.
- :has() is the parent selector where it allows us to style an element based on what is happening inside or immediately after it.
- :not() is the exclusion selector that do not match the selector inside.

7. Why choose SCSS over CSS?
- SCSS includes programming-like features such as variables, nesting, mixins, functions on top of CSS, which makes it more maintainable, reusable and scalable when working on large projects.
- Partial is a smaller, separate CSS/SCSS file that can contain specific snippets of code and can be imported and used in main stylesheet. It's name must start with underscore _ indicate it to not be compiled yet unless used with another file.

8. What are some common considerations when adapting for different screen sizes?
- Defining logical breakpoints
- Layouts with relative units for fluidity.
- Flexible typography - use rem/em or clamp() for scaling font-sizes
- Images & Media - responsiveness (max-width: 100%, srcset, <picture>)
- Mobile-first approach
- Navigation menus/patterns.
- Testing.

9. What does it mean for a browser to repaint and reflow?
- repaint - occurs when change affects visual appearance but not layout.
- reflow - occurs when change affects structure, position, size.

10. Why might a developer choose to implement aspects of a UI in Javascript over HTML or CSS files, such as animations?
- When content or styles depend on runtime data, user input or state that can't be known at build time.
- Interactivity & state.

11. What is the CSS Box Model, and how do content-box and border-box differ?
- Every element is considered a layered box in CSS. There are 4 key layers - Margin, border, padding, content.
- content-box is the default box-sizing option - width and height applies to content only, padding and border are added on top
- border-box is an option where the width and height includes padding and border.

12. What is the difference between an ID selector and a Class selector in terms of performance and usage?
- ID has a higher specificity than classes.
- In modern browsers, performance is negligible.

13. How does the Cascade work in CSS?
- The cascade is the algorithm browsers uses to determine which css rule should apply when multiple rules targets the same element.

14. What are Pseudo-classes (e.g., :hover) vs. Pseudo-elements (e.g., ::before)?
- Pseudo-classes - targets elements based on state or position. No new element is created. Eg. :hover, :focus, :active
- Pseudo-elements - Creates or targets a specific part of an element. ::before, ::after.

15. Explain the purpose of the Attribute Selector (e.g., [type="text"]).
- Targets elements based on their html values/attributes rather than creating classes or IDs.
- Specificity same as class selector (0 0 1 0).

16. What's the purpose of Combinator Selector?
- CSS combinators are used to define relationships between selectors, allowing you to select HTML elements based on their hierarchy or position relative to other elements in the document structure / Combinators allows us to select elements based on location of it relative to other elements.
    - Descendent - space - any nested level deep
    - Child - > - direct child only
    - General Sibling - ~ - all siblings after
    - Adjacent Sibling - + - immediately next sibling only

17. What is the Universal Selector (*), and what are the performance implications of using it?
- Universal selectors matches every element in the DOM.
- Impact negligible in modern browsers.

18. What is WCAG?
- It stands for Web Content Accessibility Guidelines.
- Information should be percievable by users. (eg. alt text for images)
- Interface must be operable by keyboard users.
- It must be understandable.
- Good color contrast combined with shape or text.

19. How to implement a CSS reset and why it is useful?
- CSS reset is a collection of rules that removes/normalizes the default browser styles applied to HTML elements.
- Both CSS reset and normalize css aims to solve browser inconsistencies.

20. What is margin collapsing?
- Margin collapsing can occur when there are two adjacent vertical margins. It takes the larger of the two as collapsed margin.
- Vertical margins collapses, but not horizontal margins.

21. What are css positions?
- CSS positions defines how an element is positioned within the document. Some of its properties are: 
    - static: default value, normal flow of the page.
    - relative: similar to static, but has position properties (top,right,bottom,left)
    - absolute: removed from its normal flow. positioned relative to its closest ancestor.
    - fixed: also removed from its normal flow. positioned relative to the viewport.
    - sticky: hybrid of relative and fixed. Acts relative until threshold and then its fixed.

22. Describe z-index and how is stacking order controlled.
- It controls the depth-order of elements in the z-index.(to or away from user).
- Higher the z-index, higher they are stacked.

23. Define flexbox and its advantages.
- Flexbox is an one-dimensional layout model in CSS where we can arrange in rows or columns. It gives the parent container the control on how the children are spaced, sized and aligned.

24. What is grid layout?
- It is a two-dimensional layout - both columns and rows. 
- Many useful properties to manage the page's layout and the solution for complex layout with responsiveness.

25. What are data-* attributes and when would you use them?
- These are custom attributes used in html elements to store additional data in them and can be styled as well.
- Usually used to pass data from html to js or provide specific styling to css.
    ```
    <div class="expense-card" data-id="101" data-type="recurring">
        Rent Payment
    </div>

    const card = document.querySelector('.expense-card');
    console.log(card.dataset.id);   // Output: "101"
    console.log(card.dataset.type); // Output: "recurring"
    ```

26. What are void elements in HTML? Give examples
- These are HTML elements that don't have a closing tag and they cannot have child nodes.
- Examples are - <img>, <br>, <input>, <hr>

27. What input types were introduced in HTML5?
- Input type email - whether it has a proper email format, input type url, input type search.
- date and time pickers inbuilt.
- range - gives slider control.

28. What are ARIA roles and when should you use them?
- aria roles are kind of labels added to HTML to tell the screen readers what that element does.
- For example, if we build a progress bar, the screen reader will not know if you used that as a progress bar.
    ``` <div role="progressbar" aria-valuenow="70" aria-valuemin="0" aria-valuemax="100"></div> ```

29. How do you make a website keyboard navigable?
- Some of the points to keep in mind: use native elements (button, links, inputs) that have keyboard focus
- Use :focus-visible pseudoclass in css

30. How to make images responsive css?
- To make images responsive, the standard approach is to use max-width: 100% and height: auto, which allows the image to scale within its container while preserving its aspect ratio. 
- For more complex layouts where images must fill a specific area, we use object-fit: cover. From a performance perspective, we use the srcset and sizes attributes or the <picture> element to serve different image files based on the user's device resolution and screen width, ensuring faster load times and better art direction.