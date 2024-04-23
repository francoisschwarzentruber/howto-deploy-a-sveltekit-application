# How to deploy a sveltekit application

For me, it was super easy to develop a small Sveltekit application. Really, **I love Svelte**. It is super simple to use. But it was **horribly difficult** to deploy it on a github page. Here I explain how I finally succeeded.

## Setup your application project

The standard routine is:

 ```
npm create svelte@latest my-app
cd my-app
npm install
npm run dev -- --open
```

This works like a charm.

## The adapter thing

Sveltekit uses a thing called an adapter. I do not really understand what it is, and honestly, I do not care. I just want it to work. In `svelte.config`, add:

          	import adapter from '@sveltejs/adapter-static';

		adapter: adapter({
			// default options are shown. On some platforms
			// these options are set automatically — see below
			pages: 'build',
			assets: 'build',
			fallback: "index.html",
			precompress: false,
			strict: false
		})
		`

In the documentation, it is written `fallback: undefined` I do not know why. But this is not working since it is not producing `index.html`. The line `strict: false` is for avoiding a strange error. I did not spend time to understand this strange error but `strict: false` works like a charm.




## Setup for github pages

- In `svelte.config.js`, add:

		paths: {
			base: process.env.NODE_ENV === 'production' ? '/replace-by-the-name-of-your-app' : '',
		}


- Do `npm install gh-pages`.
- Add `"deploy": "npm run build && npx gh-pages -d build -t true"` as a script in `package.json`.
- Add a file named `.nojekyll` in the `gt-pages` branch (not the `main` one!)

- By running `npm run deploy` it will compile your project and deploy your application to the `gt-pages` branch.
