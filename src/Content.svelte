<script>
  import { getContext } from 'svelte';
  import Popup from './Popup.svelte';
  const { open } = getContext('simple-modal');
  export let char;
  const showSurprise = () => open(Popup, { char: char });
</script>

<p><button on:click={showSurprise} class="hover:underline font-normal">Show more info</button></p>
  

