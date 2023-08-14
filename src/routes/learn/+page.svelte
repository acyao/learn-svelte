<script lang="ts">
    import { text } from '@sveltejs/kit';
    import type { PageData } from './$types';
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

    function subscribe(){
        alert('Good Luck! HAHA! Sending email spam to ' + textbox1);
    }
</script>

<p>{word}</p>
<img {src} alt={name} style="height: 50%; width:50%" />

<input style="width: 20%;" bind:value={textbox1} type="email"/>

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

<button disabled={!checkbox1} on:click={subscribe}>Subscribe</button>

