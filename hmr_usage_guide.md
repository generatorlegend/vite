# Hot Module Replacement (HMR) Usage Guide

Hot Module Replacement (HMR) is a powerful feature in Vite that allows you to update your application in real-time without a full page reload. This guide will help you understand how to effectively use HMR in your Vite projects.

## Table of Contents

1. [Introduction to HMR](#introduction-to-hmr)
2. [Enabling HMR](#enabling-hmr)
3. [HMR for Different File Types](#hmr-for-different-file-types)
4. [Writing HMR-friendly Code](#writing-hmr-friendly-code)
5. [Best Practices](#best-practices)
6. [Troubleshooting](#troubleshooting)

## Introduction to HMR

Hot Module Replacement (HMR) significantly improves the development experience by allowing you to see changes in your application instantly without losing the current state. When you make changes to your code, Vite will update only the affected modules, preserving the rest of your application's state.

Benefits of using HMR:
- Faster development cycle
- Preserved application state during updates
- Improved debugging experience

## Enabling HMR

Vite enables HMR by default for many file types. However, you may need to add some code to your application to handle updates properly.

To enable HMR for your JavaScript modules, you can use the `import.meta.hot` API:

```javascript
if (import.meta.hot) {
  import.meta.hot.accept((newModule) => {
    // Handle hot update
  })
}
```

## HMR for Different File Types

### JavaScript

For JavaScript files, you can use the `import.meta.hot.accept()` method to handle updates:

```javascript
if (import.meta.hot) {
  import.meta.hot.accept((newModule) => {
    // Replace old module implementation with new one
  })
}
```

### CSS

CSS files are hot reloaded out of the box. When you make changes to a CSS file, Vite will automatically update the styles without a full page reload.

### Vue Single File Components

Vue SFCs (`.vue` files) support HMR by default when using the `@vitejs/plugin-vue` plugin. No additional configuration is required.

### React

For React components, you can use the `import.meta.hot.accept()` method along with a library like `react-refresh` to enable HMR:

```javascript
import { useState } from 'react'

const MyComponent = () => {
  const [count, setCount] = useState(0)
  return <button onClick={() => setCount(count + 1)}>{count}</button>
}

export default MyComponent

if (import.meta.hot) {
  import.meta.hot.accept()
}
```

## Writing HMR-friendly Code

To make the most of HMR, consider the following tips when writing your code:

1. Use `import.meta.hot.accept()` to handle updates for specific modules.
2. Keep your state management separate from your UI components.
3. Use `import.meta.hot.dispose()` to clean up side effects when a module is replaced.

Example of using `dispose`:

```javascript
if (import.meta.hot) {
  const interval = setInterval(() => {
    // Some operation
  }, 1000)

  import.meta.hot.dispose(() => {
    clearInterval(interval)
  })
}
```

## Best Practices

1. Use HMR selectively: Only enable HMR for modules that truly benefit from it.
2. Keep your modules small and focused: This makes it easier to hot-replace specific parts of your application.
3. Avoid storing state in global variables: Use state management libraries or local component state instead.
4. Use `import.meta.hot.data` to preserve state across module replacements:

```javascript
if (import.meta.hot) {
  import.meta.hot.data.count = import.meta.hot.data.count || 0

  import.meta.hot.accept((newModule) => {
    newModule.count = import.meta.hot.data.count
  })
}
```

5. Use the `vite:beforeUpdate` and `vite:afterUpdate` events to perform actions before and after HMR updates:

```javascript
if (import.meta.hot) {
  import.meta.hot.on('vite:beforeUpdate', () => {
    console.log('About to update module')
  })

  import.meta.hot.on('vite:afterUpdate', () => {
    console.log('Module updated')
  })
}
```

## Troubleshooting

If you encounter issues with HMR:

1. Check the browser console for error messages.
2. Ensure that your code is properly handling HMR updates.
3. Verify that you're using the latest version of Vite and its plugins.
4. Try clearing the browser cache and restarting the Vite dev server.
5. If using a framework, consult its specific HMR documentation for any additional setup required.

Remember that some changes, like adding new CSS rules or modifying the HTML structure, may still require a full page reload to take effect.

By following this guide, you should be able to effectively use Hot Module Replacement in your Vite projects, leading to a more efficient and enjoyable development experience.