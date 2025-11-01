# Finance Encyclopedia - Design Guide

This document provides comprehensive instructions for customizing and updating the design of the Finance Encyclopedia flashcard application.

## Table of Contents
1. [Design Philosophy](#design-philosophy)
2. [New Features](#new-features)
3. [Color Customization](#color-customization)
4. [Typography](#typography)
5. [Layout & Spacing](#layout--spacing)
6. [Component Customization](#component-customization)
7. [Responsive Design](#responsive-design)
8. [Adding New Features](#adding-new-features)

---

## Design Philosophy

The current design follows these principles:
- **Minimal**: Clean, distraction-free interface
- **High Contrast**: Black and white theme for maximum readability
- **Readable**: Large text sizes (18px base, up to 48px for headings)
- **Responsive**: Adapts seamlessly from mobile to desktop
- **Fast**: No external dependencies except Google Fonts (Inter)

---

## New Features

### Search Functionality
The application now includes a powerful search feature that filters cards in real-time:

**How it works:**
- Type in the search bar to filter cards by title, explanation, or topic
- Search is case-insensitive and matches partial words
- Results update instantly as you type
- Click the "×" button to clear the search
- Random card generation works with search results (generates random cards from filtered results)

**Customizing the search bar:**

Location: `style.css` - `.search-container` section

```css
.search-container input[type="text"] {
    font-size: var(--font-size-lg);     /* Change text size */
    padding: var(--spacing-md);          /* Adjust padding */
    border: 2px solid var(--color-border); /* Border style */
}
```

### Dark Theme Toggle
A theme switcher button allows users to toggle between light and dark modes:

**Features:**
- Click the sun icon button to switch themes
- Dark theme: Black background with white text (reduces eye strain)
- Light theme: White background with black text (default)
- Theme preference is saved in browser localStorage
- Automatically loads saved preference on page reload

**How the dark theme works:**

The dark theme uses CSS custom properties to invert colors:

```css
body.dark-theme {
    --color-bg: #000000;        /* Black background */
    --color-text: #ffffff;      /* White text */
    --color-border: #ffffff;    /* White borders */
    --color-hover-bg: #ffffff;  /* White hover background */
    --color-hover-text: #000000; /* Black hover text */
}
```

**Customizing the dark theme:**

You can adjust the dark theme colors in `style.css` (around line 449):

```css
/* Example: Dark gray theme instead of pure black */
body.dark-theme {
    --color-bg: #1a1a1a;
    --color-text: #f0f0f0;
    --color-border: #cccccc;
    --color-hover-bg: #f0f0f0;
    --color-hover-text: #1a1a1a;
}
```

**Removing the theme toggle:**

If you want only one theme, remove the theme button from `index.html` (lines 38-47) and remove the dark theme CSS.

---

## Color Customization

All colors are defined using CSS custom properties (variables) in `style.css`. Find them at the top of the file:

```css
:root {
    --color-bg: #ffffff;           /* Background color */
    --color-text: #000000;         /* Text color */
    --color-border: #000000;       /* Border color */
    --color-hover-bg: #000000;     /* Hover background */
    --color-hover-text: #ffffff;   /* Hover text color */
}
```

### How to Change Colors

**Example 1: Dark Mode**
```css
:root {
    --color-bg: #000000;
    --color-text: #ffffff;
    --color-border: #ffffff;
    --color-hover-bg: #ffffff;
    --color-hover-text: #000000;
}
```

**Example 2: Soft Gray Theme**
```css
:root {
    --color-bg: #f5f5f5;
    --color-text: #1a1a1a;
    --color-border: #333333;
    --color-hover-bg: #333333;
    --color-hover-text: #f5f5f5;
}
```

**Example 3: Blue Accent**
```css
:root {
    --color-bg: #ffffff;
    --color-text: #0a0a0a;
    --color-border: #0066cc;
    --color-hover-bg: #0066cc;
    --color-hover-text: #ffffff;
}
```

---

## Typography

### Current Font
The application uses **Inter** font from Google Fonts, known for excellent readability.

### Font Sizes
All font sizes are defined as CSS variables:

```css
:root {
    --font-size-base: 18px;    /* Body text */
    --font-size-lg: 22px;      /* Large text, buttons */
    --font-size-xl: 28px;      /* Card titles */
    --font-size-2xl: 36px;     /* Modal titles */
    --font-size-3xl: 48px;     /* Main heading */
}
```

### How to Change Font

**Option 1: Use a Different Google Font**

1. Go to [Google Fonts](https://fonts.google.com/)
2. Select your font (e.g., "Roboto", "Open Sans", "Poppins")
3. Copy the `<link>` tag
4. Replace the font link in `index.html` (lines 8-10):

```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

5. Update the font-family in `style.css` (line 23):

```css
font-family: 'Roboto', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
```

**Option 2: Use System Fonts (Faster Loading)**

Remove the Google Fonts link from `index.html` and update `style.css`:

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
```

### How to Adjust Font Sizes

To make text larger or smaller, modify the variables in `:root`:

**Larger Text (for better accessibility):**
```css
:root {
    --font-size-base: 20px;
    --font-size-lg: 24px;
    --font-size-xl: 32px;
    --font-size-2xl: 40px;
    --font-size-3xl: 56px;
}
```

**Smaller Text (more compact):**
```css
:root {
    --font-size-base: 16px;
    --font-size-lg: 18px;
    --font-size-xl: 24px;
    --font-size-2xl: 30px;
    --font-size-3xl: 40px;
}
```

---

## Layout & Spacing

### Spacing System
Consistent spacing is maintained using CSS variables:

```css
:root {
    --spacing-xs: 0.5rem;   /* 8px */
    --spacing-sm: 1rem;     /* 16px */
    --spacing-md: 1.5rem;   /* 24px */
    --spacing-lg: 2rem;     /* 32px */
    --spacing-xl: 3rem;     /* 48px */
}
```

### Card Grid Layout

Cards use CSS Grid for responsive layout. Find this in `style.css` (line 155):

```css
#card-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: var(--spacing-lg);
}
```

**To change card width:**
- Smaller cards: Change `350px` to `280px`
- Larger cards: Change `350px` to `450px`

**To change gap between cards:**
```css
gap: var(--spacing-xl);  /* Larger gap */
gap: var(--spacing-sm);  /* Smaller gap */
```

### Container Width

The main container has a max-width of 1400px. To change it, edit line 54:

```css
.container {
    max-width: 1200px;  /* Narrower */
    /* or */
    max-width: 1600px;  /* Wider */
}
```

---

## Component Customization

### Cards

**Card Border Style**

Current: 2px solid border
```css
.card {
    border: 2px solid var(--color-border);
}
```

Options:
```css
border: 1px solid var(--color-border);     /* Thinner */
border: 3px solid var(--color-border);     /* Thicker */
border: none;                               /* No border */
box-shadow: 0 2px 8px rgba(0,0,0,0.1);    /* Shadow instead */
```

**Card Hover Effect**

Current: Shadow offset effect
```css
.card:hover {
    box-shadow: 8px 8px 0 var(--color-text);
    transform: translate(-4px, -4px);
}
```

Alternative effects:
```css
/* Subtle lift */
.card:hover {
    transform: translateY(-4px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

/* Scale up */
.card:hover {
    transform: scale(1.02);
}

/* No effect */
.card:hover {
    /* Remove all properties */
}
```

### Buttons

**Button Style**

Buttons use the same black/white theme. To customize:

```css
.primary-btn {
    background-color: var(--color-text);
    color: var(--color-bg);
    border-radius: 4px;  /* Change to 8px for rounder corners */
}
```

**Button Sizes**

```css
.primary-btn {
    padding: var(--spacing-lg) var(--spacing-xl);  /* Larger */
    padding: var(--spacing-xs) var(--spacing-md);  /* Smaller */
}
```

### Modal

**Modal Size**

```css
.modal-content {
    max-width: 800px;  /* Current */
    max-width: 600px;  /* Smaller */
    max-width: 1000px; /* Larger */
}
```

**Modal Background Blur**

```css
.modal {
    background-color: rgba(0, 0, 0, 0.85);  /* Current: 85% opacity */
    background-color: rgba(0, 0, 0, 0.95);  /* Darker */
    backdrop-filter: blur(4px);              /* Blur amount */
}
```

---

## Responsive Design

The design includes three breakpoints:

### Desktop (Default)
- Full grid layout
- Large text sizes
- Horizontal flashcard selector

### Tablet (≤768px)
- Single column cards
- Slightly smaller text
- Vertical flashcard selector

### Mobile (≤480px)
- Optimized for small screens
- Smallest text sizes
- Full-width buttons

### How to Adjust Breakpoints

Edit the media queries in `style.css` (lines 290-367):

```css
@media (max-width: 768px) {
    /* Tablet styles */
}

@media (max-width: 480px) {
    /* Mobile styles */
}
```

To add a new breakpoint:

```css
@media (max-width: 1024px) {
    /* Large tablet styles */
    #card-container {
        grid-template-columns: repeat(2, 1fr);
    }
}
```

---

## Adding New Features

### Adding More Cards

Edit `cards.json` and add new entries:

```json
{
    "title": "Your Topic",
    "topic": "Category",
    "buttonText": "Learn More",
    "explanation": "Detailed explanation here..."
}
```

### Adding a Footer

Add before the closing `</body>` tag in `index.html`:

```html
<footer style="text-align: center; padding: 2rem; border-top: 2px solid var(--color-border);">
    <p>© 2024 Finance Encyclopedia</p>
</footer>
```

### Adding Categories Filter

This would require JavaScript modifications. Add a filter section in HTML and update the `displayCards()` function to filter by topic.

### Changing the GitHub Link

Update line 14 in `index.html`:

```html
<a href="https://github.com/YOUR-USERNAME/YOUR-REPO" target="_blank" class="github-link">
```

---

## Quick Customization Checklist

- [ ] Update GitHub repository link in `index.html` (line 14)
- [ ] Change color scheme in `style.css` `:root` variables
- [ ] Customize dark theme colors if needed
- [ ] Adjust font sizes if needed
- [ ] Customize card hover effects
- [ ] Add your content to `cards.json`
- [ ] Test search functionality with your content
- [ ] Test dark theme toggle
- [ ] Test on mobile devices
- [ ] Update page title in `index.html` (line 6)

---

## Tips for Best Results

1. **Always test changes on multiple screen sizes** - Use browser dev tools
2. **Keep contrast high** - Ensure text is readable
3. **Use consistent spacing** - Stick to the spacing variables
4. **Optimize fonts** - Limit font weights to keep loading fast
5. **Validate your JSON** - Use a JSON validator when editing `cards.json`

---

## Need Help?

- CSS Variables: [MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- CSS Grid: [CSS-Tricks Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- Google Fonts: [fonts.google.com](https://fonts.google.com/)

---

**Last Updated:** 2024
**Version:** 2.0

