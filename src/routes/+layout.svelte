<script lang="ts">
	import type { LayoutProps } from './$types'
	import { assets } from '$app/paths'
    import Navmenu from './Navmenu.svelte'
	import Footer from './Footer.svelte';

	let { children }: LayoutProps = $props()
</script>

<svelte:head>
    <link href="https://unpkg.com/sanitize.css" rel="stylesheet" />

    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Montserrat">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Open+Sans">

    <link rel="stylesheet" href="{assets}/css/theme-default.css" />
</svelte:head>

<Navmenu></Navmenu>

<main class="container">
    {@render children()}
</main>

<Footer></Footer>

<style>
    .container {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>