# NOTES

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

Install `tailwindcss` and its peer dependencies via npm, and then run the init command to generate both `tailwind.config.js` and `postcss.config.js.`

```shell
$ npm install -D tailwindcss postcss autoprefixer
# generate tailwind and postcss config files
$ npx tailwindcss init -p
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

`src/index.css`

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





npm i -D concurrently


  "scripts": {
    "dev": "concurrently \"yarn tailwind:css\" \"yarn start\"",
    "tailwind:css": "postcss ./src/styles/tailwind.css -o ./src/styles/index.css --watch",





You are running `create-react-app` 4.0.3, which is behind the latest release (5.0.0).

We no longer support global installation of Create React App.

Please remove any global installs with one of the following commands:
- npm uninstall -g create-react-app
- yarn global remove create-react-app


npx clear-npx-cache
sudo npm uninstall -g create-react-app
sudo npm install -g create-react-app
create-react-app --version
5.0.0

