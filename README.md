# BUILD-TOOLS-BUCHELI-COURSE-VITE-REACT-PROJECT

## Building Apps with Vite
Learn how to build a web app using Vite.

In this article, we will use Vite to bundle an existing web app. Vite may be the right build tool for you if your project contains many modules as it can bundle files at
lightning speed by pre-bundling dependencies.

Vite makes it easy to start a project as it comes with template presets for projects using vanilla JavaScript, as well as frameworks such as Vue, React, Preact, Svelte, and 
Typescript. Vite also provides Hot Module Replacement, which is automatically configured when a project is created using create-vite. The functionalities of Vite can be easily
extended by using plugins.

## Project Setup
Remember that you can initialize Node.js using:

```
npm init -y
```

The project is already a Node.js project. But you will need to install the dependencies that are in the package.json file by running the following command:

```npm install
```

Next, you will need to install Vite as well as react-refresh to add HMR support by running:

```
npm install vite @vitejs/plugin-react-refresh 
```

## Vite Config File
In order to properly use Vite, you will need to create a vite.config.js file in the root of your project. This file will contain the configuration for your project, including
any additional plugins that your project may require.

Add the following code to your vite.config.js file:

```
import { defineConfig } from 'vite';
import reactRefresh from '@vitejs/plugin-react-refresh';
 
export default defineConfig({
  plugins: [reactRefresh()]
});
```

In the configuration file, we are using a plugin called react-refresh() from @vitejs/plugin-react-refresh. This plugin will be used to refresh the page when you make a change
to a react component.

## The Build and Serve Commands
Let’s add our start, build, and serve commands in the "scripts" section of package.json. These commands are use to serve a development build of our app, build a production
build, or serve the production build of our app locally.

```
"scripts": {
  "start": "vite",
  "build": "vite build",
  "serve": "vite preview"
}
```

In the code block above, the build command runs with the default entry point at ./index.html to bundle the app with the exit point at ./dist. When the serve command is ran, the
project is served from ./dist.

Remember that you can run the build, start, or serve commands with npm run X, where X is our custom script.

If you are following along with the starting code of our React app, you will notice that running npm run start will produce the following error:

 ```
 > src/app.js:31:11: error: Unexpected "<"
    31 │     return <Carousel src={PATHS[currentImg]} />
       ╵            ^   
```

This error is caused by Vite encountering JSX code in a JavaScript file. We will address this in the next section.

## JSX
Our scripts will throw errors because our Carousel.js contains JSX. Vite supports JSX, but files containing JSX must have the .jsx extension. If you are following along using the provided starting code, you will need to change the file extension of both App.js and Carousel.js to .jsx.

The file structure of ./src should now look like this:

```
|-- src
|   |-- app.jsx
|   |-- Carousel.CSS
|   |-- Carousel.jsx
|   |-- sun.svg
```

You will also need to edit the value of the src attribute of the <script> tag in ./index.html from '/src/app.js' to '/src/app.jsx' to reflect the change in file extension.

```
<script type="module" src="/src/app.jsx"></script>
```

## CSS
When CSS files are imported directly in JavaScript using the import statement, Vite will automatically gather all referenced CSS files and bundle them into a single CSS file at the exit point.

You will see that in the provided starting code we import Carousel.css in Carousel.js like below:

```
import './Carousel.css';
```

Vite doesn’t need any plugins or config options specified in order to automatically bundle Carousel.css file at the exit point at ./dist.

## Putting It All Together
Now that we’ve configured our vite.config.js file, file extensions, and package.json, running the build command should generate bundled files of the project in ./dist. Notice that the files in the src directory have been bundled and linked in ./dist/index.html .

To view the bundled app in ./dist, you will need to run:

```
npm run serve
```

In this article, we discussed how to use Vite to quickly build your application and utilize its extensive plugin system. Next time you’re building a web app on your own, consider using Vite!

## Take a look at the live project here:
https://bucheli-web-build-tools-vite-react-project.netlify.app/
