# How to deploy a sveltekit application

For me, it was super easy to develop a small Sveltekit application. Really, I love Svelte. It is super simple to use. But it was **horribly difficult** to deploy it on a github page.

## Setup your application project

 ```
npm create svelte@latest my-app
cd my-app
npm install
npm run dev -- --open
```

## The adapter thing

Sveltekit uses a thing called an adapter. I do not really understand what it is and I do not care. I just want it to work. In `svelte.config`, add:

`import adapter from '@sveltejs/adapter-static';

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

In the documentation, it is written `fallback: undefined` I do not know why. But it is not working since it is not producing `index.html`. The line `strict: false` is for avoiding a strange error.


