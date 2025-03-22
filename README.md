# Toast Notifications Testing

Investigating a class based toast system using the HTML Popover API + Anchor CSS positioning.

## Features

- Automatic positioning with CSS anchor positioning
- Simple open/close animations
- No JavaScript required for core functionality

## Usage

1. Click any button in the control panel to display a notification
2. Notifications stack in sequence from bottom-left (can change this easily)
3. Close with the "✕" button or toggle with the same control button

## Known Issues
- no stacking on mobile ?? or safari 
- the css indexing get out of order (but the total is still correct)
- No exit animation 

## Technical Notes

The key to this working is the sequence in which CSS properties are processed and applied. The CSS engine processes declarations in the following order:

First, the element reads the existing --previous-item anchor in the DOM (if one exists)
Then, it positions itself relative to that anchor using position-anchor: --previous-item, top: anchor(bottom), etc.
Finally, it sets itself as the new --previous-item with anchor-name: --previous-item

This creates a chain where:

The first popover that opens doesn't find a --previous-item anchor, so it positions itself at the default location
When the second popover opens, it anchors to the first one (which now has the --previous-item name)
Then the second popover becomes the new --previous-item
And so on for subsequent popovers

This works because the property values are computed in a single pass before being applied to the layout. The element reads the current state of the DOM for positioning itself, and only after that does it update its own anchor name.

### Browser Support

Requires browsers that support the HTML Popover API and CSS anchor positioning.

## Relevant CSS

```css
.toast:popover-open {
    position: absolute;
    position-area: top span-left;
    
    /* Connect to the previous element's anchor */
    position-anchor: --previous-item;
    
    /* Position below the previous element with margin */
    top: anchor(bottom);
    right: anchor(left);
    
    /* Become the new anchor for the next element */
    anchor-name: --previous-item;
}
```

<img width="571" alt="Screenshot 2025-03-21 at 9 13 22 PM" src="https://github.com/user-attachments/assets/8f744570-33f1-4dbc-8086-fd5e3afd1781" />

