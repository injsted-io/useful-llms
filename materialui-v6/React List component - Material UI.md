## Lists

Lists are continuous, vertical indexes of text or images.

Lists are a continuous group of text or images. They are composed of items containing primary and supplemental actions, which are represented by icons and text.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20list)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/List)
-   [Material Design](https://m2.material.io/components/lists)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/all-components/#introduction)

Lists present information in a concise, easy-to-follow format through a continuous, vertical index of text or images.

Material UI Lists are implemented using a collection of related components:

-   List: a wrapper for list items. Renders as a `<ul>` by default.
-   List Item: a common list item. Renders as an `<li>` by default.
-   List Item Button: an action element to be used inside a list item.
-   List Item Icon: an icon to be used inside of a list item.
-   List Item Avatar: an avatar to be used inside of a list item.
-   List Item Text: a container inside a list item, used to display text content.
-   List Divider: a separator between list items.
-   List Subheader: a label for a nested list.

___

-   [
    
    Spam
    
    ](https://v6.mui.com/material-ui/all-components/#simple-list)

The last item of the previous demo shows how you can render a link:

```jsx
<ListItemButton component="a" href="#simple-list"> <ListItemText primary="Spam" /> </ListItemButton>
```

You can find a [demo with React Router following this section](https://v6.mui.com/material-ui/integrations/routing/#list) of the documentation.

## [Basics](https://v6.mui.com/material-ui/all-components/#basics)

```jsx
import List from '@mui/material/List'; import ListItem from '@mui/material/ListItem';
```

## [Nested List](https://v6.mui.com/material-ui/all-components/#nested-list)

## [Folder List](https://v6.mui.com/material-ui/all-components/#folder-list)

## [Interactive](https://v6.mui.com/material-ui/all-components/#interactive)

Below is an interactive demo that lets you explore the visual results of the different settings:

Enable denseEnable secondary text

Text only

-   Single-line item
    
-   Single-line item
    
-   Single-line item
    

Icon with text

-   Single-line item
    
-   Single-line item
    
-   Single-line item
    

Avatar with text

-   Single-line item
    
-   Single-line item
    
-   Single-line item
    

Avatar with text and icon

-   Single-line item
    
-   Single-line item
    
-   Single-line item
    

## [Selected ListItem](https://v6.mui.com/material-ui/all-components/#selected-listitem)

## [Align list items](https://v6.mui.com/material-ui/all-components/#align-list-items)

When displaying three lines or more, the avatar is not aligned at the top. You should set the `alignItems="flex-start"` prop to align the avatar at the top, following the Material Design guidelines:

-   ![Remy Sharp](https://v6.mui.com/static/images/avatar/1.jpg)
    
    Brunch this weekend?
    
    Ali Connors — I'll be in your neighborhood doing errands this…
    

-   ![Travis Howard](https://v6.mui.com/static/images/avatar/2.jpg)
    
    Summer BBQ
    
    to Scott, Alex, Jennifer — Wish I could come, but I'm out of town this…
    

-   ![Cindy Baker](https://v6.mui.com/static/images/avatar/3.jpg)
    
    Oui Oui
    
    Sandra Adams — Do you have Paris recommendations? Have you ever…
    

## [List Controls](https://v6.mui.com/material-ui/all-components/#list-controls)

### [Checkbox](https://v6.mui.com/material-ui/all-components/#checkbox)

A checkbox can either be a primary action or a secondary action.

The checkbox is the primary action and the state indicator for the list item. The comment button is a secondary action and a separate target.

The checkbox is the secondary action for the list item and a separate target.

-   ![Avatar n°1](https://v6.mui.com/static/images/avatar/1.jpg)
    
    Line item 1
    
-   ![Avatar n°2](https://v6.mui.com/static/images/avatar/2.jpg)
    
    Line item 2
    
-   ![Avatar n°3](https://v6.mui.com/static/images/avatar/3.jpg)
    
    Line item 3
    
-   ![Avatar n°4](https://v6.mui.com/static/images/avatar/4.jpg)
    
    Line item 4
    

### [Switch](https://v6.mui.com/material-ui/all-components/#switch)

The switch is the secondary action and a separate target.

Upon scrolling, subheaders remain pinned to the top of the screen until pushed off screen by the next subheader. This feature relies on CSS sticky positioning.

## [Inset List Item](https://v6.mui.com/material-ui/all-components/#inset-list-item)

The `inset` prop enables a list item that does not have a leading icon or avatar to align correctly with items that do.

## [Gutterless list](https://v6.mui.com/material-ui/all-components/#gutterless-list)

When rendering a list within a component that defines its own gutters, `ListItem` gutters can be disabled with `disableGutters`.

-   Line item 1
    
-   Line item 2
    
-   Line item 3
    

Press Enter to start editing

## [Virtualized List](https://v6.mui.com/material-ui/all-components/#virtualized-list)

In the following example, we demonstrate how to use [react-window](https://github.com/bvaughn/react-window) with the `List` component. It renders 200 rows and can easily handle more. Virtualization helps with performance issues.

Press Enter to start editing

The use of [react-window](https://github.com/bvaughn/react-window) when possible is encouraged. If this library doesn't cover your use case, you should consider using alternatives like [react-virtuoso](https://github.com/petyosi/react-virtuoso).

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

[

🔥

Firebash

](https://v6.mui.com/material-ui/all-components/#customized-list)

___

___

Build

Authentication, Firestore Database, Realtime Database, Storage, Hosting, Functions, and Machine Learning