## Sveltekit Template for Docker

This is a template for a Sveltekit project that can be run in a Docker container.

The project uses Skeleton.ui (https://www.skeleton.dev/docs/get-started) for styling.

### How this template was created

Create Sveltekit project using the Skeleton cli:
```
npm create skeleton-app@latest sveltekit-template
```

Install node-adapter as a development dependency: 
``` bash
yarn add @sveltejs/adapter-node --dev
````

Modify the `svelte.config.js` file by replacing:
```javascript
import adapter from '@sveltejs/adapter-auto';
```
with
```javascript
import adapter from '@sveltejs/adapter-node';
```

Install all dependencies:
```javascript
yarn install
```

Build the project:
```javascript
yarn build
```

At this stage we can launch our project (locally) to check if everything is working:
```bash
node build/index.js
```

Now we can create a Docker image. For this in our `Dockerfile` we do it in 2 stages:
First we define a builder image. This image will be used to build our project. This is basically doing the steps that we had manually done above.
Then we define a runtime image. This image will be used to run our project. 
In this case we copy the build folder from the builder image, run `yarn install --production` and then run `node build/index.js`.


The `.dockerignore` file contains:
```
build
node_modules
.svelte-kit
.env
```

Now, if we clone this repo and we want to replicate this we need to run the commands below before building the image:
```bash
yarn install
yarn build
```


