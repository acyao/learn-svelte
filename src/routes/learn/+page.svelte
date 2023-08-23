<script lang="ts">
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
        document.getElementById("text1").style.display = 'block';
        
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

<p id="text1" style="display: none; font-size:30px;color:red">Thank you for let us collect and sell your data.</p>

