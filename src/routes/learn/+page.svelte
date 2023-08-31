<script lang="ts">
    import { onMount } from 'svelte';
    import { text } from '@sveltejs/kit';
    import type { PageData } from './$types';
    import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	import { page } from '$app/stores';
	import { preprocess } from 'svelte/compiler';

    export let data: PageData;

    let textbox1 = "";
    let checkbox1 = false;
    let src = 'src/lib/images/learn.jpg';
    let name = "Learn Image";
    let count = 0;
    let first = "Learn";
    let second = "Svelte";
    let word = "";
    let checkBoxColorToggle = "red";
    let posts: any[] = [];
    let visible = false;
    $: word = first + ' ' + second;
    $: count = textbox1.length * 2;
    $: checkBoxColorToggle = checkbox1 ? 'green' : 'red';


    const progress = tweened(0, {
        duration: 400,
        easing: cubicOut
    });

    function subscribe(){
        alert('Good Luck! HAHA! Sending email spam to ' + textbox1);
        progress.set(1);
        visible = true;
        console.log(visible);
    }

    onMount(async () => {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        posts = await response.json();
    })

    const handleClick = (id) => {
        console.log('id: ' +id);
        posts = posts.filter((post) => post.id != id);
        console.log(posts);
    }

</script>

<p>{word}</p>
<img {src} alt={name} style="height: 50%; width:50%; margin:20px 0px" />

<input style="width: 40%;" bind:value={textbox1} type="email" placeholder="Enter Your Email"/>

{#if textbox1.length > 0}
    <p>{count} - reactive declarations</p>
{:else}
    <p>NULL</p>
{/if}

<label>
    <input type="checkbox" bind:checked={checkbox1} />
    Send me email spam!
</label>

{#if checkbox1}
    <p style="color: {checkBoxColorToggle};">Nice! Your mailbox gonna blow up!</p>
{:else}
    <p style="color: {checkBoxColorToggle};">Please tick a checkbox!</p>
{/if}

<button style="width: 40%;" disabled={!checkbox1} on:click={subscribe}>Subscribe</button>

<progress style="width: 40%; margin: 20px 0px" value={$progress} />

{#if visible}
    <p id="text1" style="font-size:30px;color:red">Thank you for let us collect and sell your data.</p>
{/if}

{#each posts as post (post.id)}
    <h3>{post.id}. {post.title}</h3>
    <p>{post.body}</p>
    <button on:click={() =>handleClick(post.id)}>Delete</button>
{:else}
    <p>Loading...</p>
{/each}