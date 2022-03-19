# NOTES

- [NOTES](#notes)
  - [Links](#links)
  - [Extensions](#extensions)
  - [Start Project](#start-project)
  - [Install Tailwind CSS](#install-tailwind-css)
    - [Configure your template paths](#configure-your-template-paths)
    - [Add the Tailwind directives to your CSS](#add-the-tailwind-directives-to-your-css)
    - [Start your build process](#start-your-build-process)
    - [Start using Tailwind in your project](#start-using-tailwind-in-your-project)
    - [To use in dev env we can use Watch](#to-use-in-dev-env-we-can-use-watch)
  - [Add Tauri](#add-tauri)
    - [Init Tauri](#init-tauri)
    - [Development Cycle](#development-cycle)
    - [Pre Requisites](#pre-requisites)

## Links

- [Install Tailwind CSS with Create React App - Tailwind CSS](https://tailwindcss.com/docs/guides/create-react-app)
- [Adding TypeScript | Create React App](https://create-react-app.dev/docs/adding-typescript/)

## Extensions

`bradlc.vscode-tailwindcss`

## Start Project

> Start by creating a new React project with **Create React App v5.0+** if you don't have one already set up.

if we use a lower than 5.0 index.css is not post processed, I lost 1h to figure it out

```shell
# required cra 5.0
$ create-react-app --version
5.0.0

$ npx create-react-app react-with-tailwind-css-typescript --template typescript

$ mv react-with-tailwind-css-typescript ReactCRAWithTailwindCssAndTypescriptOficial

$ npm i
$ git add .
$ git commit -am "first commit"
```

## Install Tailwind CSS

- [Tailwindcss.com installation](https://tailwindcss.com/docs/installation)

Install `tailwindcss` and its peer dependencies via npm, and then run the init command to generate both `tailwind.config.js` and `postcss.config.js.`

```shell
$ npm install -D tailwindcss
# generate tailwind and postcss config files
$ npx tailwindcss init
# generate full Config
$ npx tailwindcss init --full tailwind.config-full.js
```

### Configure your template paths

Add the paths to all of your template files in your tailwind.config.js file.
`tailwind.config.js`

```javascript
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### Add the Tailwind directives to your CSS

Add the `@tailwind` directives for each of Tailwind’s layers to your `./src/index.css` file.

`src/input.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Start your build process

Run your build process with npm run start.
Terminal

```shell
$ npm run start
./src/App.css (./node_modules/css-loader??ref--6-oneOf-3-1!./node_modules/postcss-loader/src??postcss!./src/App.css)
TypeError: Cannot read properties of undefined (reading 'unprefixed')
```

### Start using Tailwind in your project

Start using Tailwind’s utility classes to style your content.

`src/App.tsx`

```typescript
function App() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  )  
}
```

### To use in dev env we can use Watch

```json
"scripts": {
  "tw:watch": "npx tailwindcss -i ./src/input.css -o ./src/index.css --watch"
}
```

## Add Tauri

- [Build smaller, faster, and more secure desktop applications with a web frontend | Tauri Studio](https://tauri.studio/)
- [Get started making desktop apps using Rust and React](https://kent.medium.com/get-started-making-desktop-apps-using-rust-and-react-78a7e07433ce)
- [Error Happened](https://www.youtube.com/watch?v=BbZmLXBDGnU)

### Init Tauri

```shell
# npm install -D @tauri-apps/cli
$ cargo install tauri-cli --locked --version ^1.0.0-rc
```

add tauri scrips

```json
{
  "tauri:dev": "cargo tauri dev",
  "tauri": "tauri",
  "bundle": "tauri build"
}
```

```shell
# init a Tauri inside the React app directory structure
$ cargo tauri init
```

### Development Cycle

```shell
$ cargo tauri dev
# or 
$ npm run tauri:dev

  --- stderr
  Package javascriptcoregtk-4.0 was not found in the pkg-config search path.
  Perhaps you should add the directory containing `javascriptcoregtk-4.0.pc'
  to the PKG_CONFIG_PATH environment variable
  Package 'javascriptcoregtk-4.0', required by 'virtual:world', not found
  Package 'javascriptcoregtk-4.0', required by 'virtual:world', not found

  --- stderr
  Package libsoup-2.4 was not found in the pkg-config search path.
  Perhaps you should add the directory containing `libsoup-2.4.pc'
  to the PKG_CONFIG_PATH environment variable
  Package 'libsoup-2.4', required by 'virtual:world', not found
  Package 'libsoup-2.4', required by 'virtual:world', not found  

warning: `"pkg-config" "--libs" "--cflags" "webkit2gtk-4.0" "webkit2gtk-4.0 >= 2.22"` did not exit successfully: exit status: 1  
```

> Once Rust has finished building, the webview opens, displaying your web app. You can make changes to your web app, and if your tooling enables it, the webview should update automatically, just like a browser. When you make changes to your Rust files, they are rebuilt automatically, and your app automatically 
> 
> restarts.

### Pre Requisites

```shell
# webkit2gtk3-devel
$ sudo zypper in webkit2gtk3-devel.x86_64 librsvg2-devel

# javascriptcoregtk
$ sudo zypper se javascriptcoregtk
$ sudo zypper in libjavascriptcoregtk-4_0-18
No update candidate for 'libjavascriptcoregtk-4_0-18-2.34.6-2.1.x86_64'. The highest available version is already installed.
# fix with
$ sudo find / -name "*javascriptcoregtk*"
# sudo ln -s /usr/lib64/libjavascriptcoregtk-4.0.so.18 /usr/lib64/libjavascriptcoregtk-4.0.so
$ rpm -qa | grep gtk | grep javascriptcoregtk
libjavascriptcoregtk-4_1-0-2.34.6-2.1.x86_64
libjavascriptcoregtk-4_0-18-2.34.6-2.1.x86_64
# fix
$ sudo zypper in libjavascriptcoregtk-5_0-0

# libsoup-2.4
$ sudo find / -name "*libsoup-2.4*"
# fix with - don't work
# sudo ln -s /usr/lib64/libsoup-2.4.so.1 /usr/lib64/libsoup-2.4.so
$ rpm -qa | grep libsoup
libsoup-devel-3.0.4-1.2.x86_64
libsoup-2_4-1-2.74.2-1.3.x86_64
libsoup-3_0-0-3.0.4-1.2.x86_64
# fix
$ sudo zypper in libsoup2-devel
```

use ubuntu machine for development

```shell
$ sudo apt update && sudo apt install libwebkit2gtk-4.0-dev \
  build-essential \
  curl \
  wget \
  libssl-dev \
  libgtk-3-dev \
  libappindicator3-dev \
  librsvg2-dev
```
