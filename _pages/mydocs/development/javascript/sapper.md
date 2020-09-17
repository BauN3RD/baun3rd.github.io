---
title: "Sapper"
permalink: /baud0wn/development/js/sapper
layout: wide
---
# Create new App
Create new app from [sapper template](https://github.com/sveltejs/sapper-template) 
## Init
Download template from GitHub
```bash
degit "sveltejs/sapper-template#rollup" my-app
```
Install dependencies
```bash
cd my-app && npm install
```
Delete unused assets, example components and routes
```bash
rm -rf ./src/routes/blog ./src/routes/about.svelte ./src/routes/index.svelte ./src/routes/_layout.svelte ./src/components/Nav.svelte ./static/global.css ./static/successkid.jpg
echo -e '<small>Little Success!</small>' > ./src/routes/index.svelte
echo -e '<main>\n\t<slot></slot>\n</main>' > ./src/routes/_layout.svelte
```
> Check if all went as expected by running the dev server on http://localhost:3000
```bash 
npm run dev
```

## Usefull stuff

### Node Modules

#### body-parser
To parse json data for requests
```bash
npm install --save body-parser
```
# Basics
## Structure
TBA
## Client-side Javascript (onMount)
To execude javascript clientside, code must be added to the onMount event loop like this:
```js
// ...
import { onMount } from 'svelte'
// ...
onMount(async () => {
		alert('Running client side now!')
});
// ...
```
## Variables

### Single file

```js
<script  context="module">
	export  async  function  preload(page, session) {
		const  name  =  'BauN3RD'
		return { name }
	}
</script>

<script>
	export  let  name  =  'BauN4RD'
// ...
	import { onMount } from  'svelte'
// ...
	onMount(async () => {
		alert(`Hello ${name}!`)
	});
// ...
</script>

<small>Little success, {name}!</small>
```
> This alterts "Hello BauN3RD!" and outputs "Little success, BauN3RD!" because `<script context="module">` fire before the page is rendered and its `return { name }` overwrites `let name = 'BauN4RD'` from the `<script>` block.

### Component to Component

We can share variables accross components by passing them to them.

`./src/components/Hello.svelte:`

```js
<script>
export  let  name  =  'BauN4RD'
</script>

Slightly bigger success, {name}!
```
`./src/routes/index.svelte`
```js
<script  context="module">
	export  async  function  preload(page, session) {
		const  name  =  'BauN3RD'
		return { name }
	}
</script>

<script>
	import { onMount } from  'svelte'
	// import component
	import  Hello  from  '../components/Hello.svelte'
// ...
	export  let  name  =  'BauN4RD'
// ...
	onMount(async () => {
		alert(`Hello ${name}`)
	});
// ...
</script>

// call 'Hello' from import and share variable 'name'
<Hello {name}/>
```
> This outputs `Slightly bigger success, BauN3RD!` and alerts `Hello BauN3RD!`

If you call `<Hello />` without passing a variable, *Hello.svelte* falls back to its default and displays `Slightly bigger success, BauN4RD` while *index.svelte* still alerts `Hello BauN3RD!`
If there is no default, it outputs `Slightly bigger success, undefined!`