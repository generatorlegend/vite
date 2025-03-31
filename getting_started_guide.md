# Getting Started with Vite

Vite is a modern frontend build tool that provides a faster and leaner development experience for modern web projects. This guide will help you get started with Vite, covering installation, project creation, basic configuration, and usage.

## Installation

To use Vite, you need to have Node.js version 14.18+ or 16+ installed. Once you have Node.js, you can install Vite using npm, yarn, or pnpm.

Using npm:

```bash
npm create vite@latest
```

Using yarn:

```bash
yarn create vite
```

Using pnpm:

```bash
pnpm create vite
```

## Creating a New Project

After running the installation command, you'll be prompted to choose a project name and select a template. Vite offers templates for various frameworks and vanilla JavaScript.

```bash
✔ Project name: · my-vite-project
✔ Select a framework: › Vue
✔ Select a variant: › JavaScript
```

Once you've made your selections, Vite will create a new project with the chosen template.

## Project Structure

A typical Vite project structure looks like this:

```
my-vite-project/
├── public/
│   └── favicon.ico
├── src/
│   ├── components/
│   ├── App.vue
│   └── main.js
├── index.html
├── package.json
└── vite.config.js
```

- `public/`: Static assets that will be served as-is
- `src/`: Your source code
- `index.html`: The entry point of your application
- `vite.config.js`: Vite configuration file

## Basic Configuration

Vite is configured using a `vite.config.js` file in the project root. Here's a basic configuration example:

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [vue()],
  server: {
    port: 3000
  },
  build: {
    outDir: 'dist'
  }
})
```

This configuration:
- Uses the Vue plugin
- Sets the development server port to 3000
- Specifies the output directory for production builds

## Starting the Development Server

To start the development server, navigate to your project directory and run:

```bash
npm run dev
```

This will start the Vite dev server, typically at `http://localhost:3000`. Vite offers fast hot module replacement (HMR) for a smooth development experience.

## Building for Production

To build your project for production, run:

```bash
npm run build
```

This command will create a production-ready build in the `dist` directory (or the directory specified in your `vite.config.js`).

## Previewing the Production Build

To preview your production build locally, you can use:

```bash
npm run preview
```

This will serve your production build, allowing you to check it before deployment.

## Next Steps

Now that you have a basic understanding of how to get started with Vite, you can explore more advanced features:

- [Configuring Vite](./config.md)
- [Using Plugins](./plugins.md)
- [Deploying a Vite Project](./deploy.md)

For more detailed information, refer to the [Vite Documentation](https://vitejs.dev/guide/).

Happy coding with Vite!