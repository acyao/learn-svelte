<script lang="ts">
    import { text } from '@sveltejs/kit';
    import type { PageData } from './$types';
    
    export let data: PageData;

    let textbox1 = "";
    let checkbox1 = false;

    function subscribe(){
        alert('Good Luck! HAHA! Sending email spam to ' + textbox1);
    }
</script>

<p>Learn</p>

<input style="width: 20%;" bind:value={textbox1} type="email"/>
<p>{textbox1}</p>

<label>
    <input type="checkbox" bind:checked={checkbox1} />
    Send me email spam!
</label>

{#if checkbox1}
    <p>Nice! Your mailbox gonna blow up!</p>
{:else}
    <p>Please tick a checkbox!</p>
{/if}

<button disabled={!checkbox1} on:click={subscribe}>Subscribe</button>