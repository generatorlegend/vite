# Configuration Options

Vite comes with a powerful and flexible configuration system that allows you to customize various aspects of your development and build process. This guide provides a detailed explanation of all available configuration options in Vite, including server options, build options, and plugin options.

## Table of Contents

- [Config File](#config-file)
- [Project Root](#project-root)
- [Base Public Path](#base-public-path)
- [Server Options](#server-options)
- [Build Options](#build-options)
- [Plugin Options](#plugin-options)
- [Dependency Pre-Bundling Options](#dependency-pre-bundling-options)
- [SSR Options](#ssr-options)

## Config File

Vite uses a configuration file named `vite.config.js` (or `.ts`) in the project root. You can use the `defineConfig` helper to get TypeScript IntelliSense for your config:

```javascript
import { defineConfig } from 'vite'

export default defineConfig({
  // Your configuration options here
})
```

## Project Root

- **Type:** `string`
- **Default:** `process.cwd()`

The project root directory. Can be an absolute path, or a path relative to the location of the config file itself.

```javascript
export default defineConfig({
  root: './src'
})
```

## Base Public Path

- **Type:** `string`
- **Default:** `/`

The base public path when served in development or production. Valid values include:

- Absolute URL pathname, e.g. `/foo/`
- Full URL, e.g. `https://foo.com/`
- Empty string or `./` (for embedded deployment)

```javascript
export default defineConfig({
  base: '/my-app/'
})
```

## Server Options

### port

- **Type:** `number`
- **Default:** `5173`

Specify server port. Note if the port is already being used, Vite will automatically try the next available port.

```javascript
export default defineConfig({
  server: {
    port: 3000
  }
})
```

### open

- **Type:** `boolean | string`
- **Default:** `false`

Automatically open the app in the browser on server start. When the value is a string, it will be used as the URL's pathname.

```javascript
export default defineConfig({
  server: {
    open: '/docs/index.html'
  }
})
```

### https

- **Type:** `boolean | https.ServerOptions`
- **Default:** `false`

Enable TLS + HTTP/2. Note this downgrades to TLS only when the `proxy` option is also used.

```javascript
export default defineConfig({
  server: {
    https: true
  }
})
```

### cors

- **Type:** `boolean | CorsOptions`
- **Default:** `false`

Configure CORS for the dev server. This is enabled by default and allows any origin. Pass an object to enable by passing options to `@koa/cors`.

```javascript
export default defineConfig({
  server: {
    cors: true
  }
})
```

## Build Options

### target

- **Type:** `string | string[]`
- **Default:** `'modules'`

Browser compatibility target for the final bundle. The default value is `'modules'`, which targets browsers with [native ES Modules](https://caniuse.com/es6-module) support.

```javascript
export default defineConfig({
  build: {
    target: 'es2015'
  }
})
```

### outDir

- **Type:** `string`
- **Default:** `dist`

Specify the output directory (relative to project root).

```javascript
export default defineConfig({
  build: {
    outDir: 'build'
  }
})
```

### assetsDir

- **Type:** `string`
- **Default:** `assets`

Specify the directory to nest generated assets under (relative to `outDir`).

```javascript
export default defineConfig({
  build: {
    assetsDir: 'static'
  }
})
```

### minify

- **Type:** `boolean | 'terser' | 'esbuild'`
- **Default:** `'esbuild'`

Set to `false` to disable minification, or specify the minifier to use. The default is [esbuild](https://github.com/evanw/esbuild).

```javascript
export default defineConfig({
  build: {
    minify: 'terser'
  }
})
```

## Plugin Options

Vite plugins can be added to the `plugins` array in the configuration file:

```javascript
import vue from '@vitejs/plugin-vue'
import legacy from '@vitejs/plugin-legacy'

export default defineConfig({
  plugins: [
    vue(),
    legacy({
      targets: ['ie >= 11']
    })
  ]
})
```

Refer to the [Vite Plugins](https://vitejs.dev/plugins/) section for more information on available plugins and how to use them.

## Dependency Pre-Bundling Options

### optimizeDeps.include

- **Type:** `string[]`

Dependencies to force include in the pre-bundle step.

```javascript
export default defineConfig({
  optimizeDeps: {
    include: ['lodash', 'vue']
  }
})
```

### optimizeDeps.exclude

- **Type:** `string[]`

Dependencies to exclude from the pre-bundle step.

```javascript
export default defineConfig({
  optimizeDeps: {
    exclude: ['your-package-name']
  }
})
```

## SSR Options

### ssr.external

- **Type:** `string[]`

Force externalize dependencies for SSR.

```javascript
export default defineConfig({
  ssr: {
    external: ['some-external-dependency']
  }
})
```

### ssr.noExternal

- **Type:** `string | RegExp | (string | RegExp)[] | true`

Prevent listed dependencies from being externalized for SSR.

```javascript
export default defineConfig({
  ssr: {
    noExternal: ['lodash-es']
  }
})
```

This comprehensive guide covers the most important configuration options available in Vite. For more detailed information and advanced options, please refer to the [official Vite documentation](https://vitejs.dev/config/).