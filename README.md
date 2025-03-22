# Toast Notification System

Investigating a class based toast system using the HTML Popover API + Anchor CSS positioning.
A lightweight, CSS-based toast notification system using the HTML Popover API.

## Features

- Five notification types: Info, Success, Warning, Error, and Critical
- Complex toast with customizable content and actions
- Automatic positioning with CSS anchor positioning
- Simple open/close animations
- No JavaScript required for core functionality

## Usage

1. Click any button in the control panel to display a notification
2. Notifications stack in sequence from top-right
3. Close with the "✕" button or toggle with the same control button

## Technical Notes

This implementation uses modern CSS features:
- HTML Popover API for managing toast state
- CSS anchor positioning for dynamic placement
- CSS animations for smooth transitions

## Browser Support

Requires browsers that support the HTML Popover API and CSS anchor positioning.

## Relevant CSS

```css
/* Subsequent visible items positioned relative to the previous one */
    .toast:popover-open {
           position: absolute;
           position-area: top span-left;

           margin-left: 1rem;
           margin-bottom: 1rem;

           /* Connect to the previous element's anchor */
           position-anchor: --previous-item;

           /* Position below the previous element with margin */
           top: anchor(bottom);
           right: anchor(left);

           /* Become the new anchor for the next element */
           anchor-name: --previous-item;

           /*counter test*/
           counter-increment: toast;
       }

       .toast::before {
           content: counter(toast);
           position: absolute;
           top: 0;
           left: 0;
           background: var(--primary);
           color: white;
           padding: 2px 4px;
           border-radius: 4px 0 0 0;
           font-size: 12px;
       }

```

<img width="571" alt="Screenshot 2025-03-21 at 9 13 22 PM" src="https://github.com/user-attachments/assets/8f744570-33f1-4dbc-8086-fd5e3afd1781" />

