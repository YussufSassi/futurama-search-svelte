<script>
	import { onMount } from 'svelte';
  import Modal from 'svelte-simple-modal';
  import Content from './Content.svelte'

  let characters;
  let query;	
  let timer;
 
  const fetchAllCharacters = async () => {
    const res = await fetch("https://futuramaapi.herokuapp.com/api/v2/characters");
    characters = await res.json()
  }
  onMount(fetchAllCharacters)

	const debounce = q => {
		clearTimeout(timer);
		timer = setTimeout(() => {
			query = q;
		}, 500);
	}

  const search = async (q) => {
      if(query) {
          const res = await fetch(`https://futuramaapi.herokuapp.com/api/v2/characters?search=${encodeURI(q)}`)
          characters = await res.json()
      } else {
        fetchAllCharacters()
      }
  }
$: search(query)
</script>
<main >
<div>
  <div class="text-center w-1/2 m-auto mt-5">
    <input type="text" class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" on:keyup={(e) => {debounce(e.target.value)}} placeholder="Search for any character">

  </div>
  {#if characters}
  <div class="characters flex gap-4 flex-row items-center justify-center flex-wrap mt-5">
    {#each characters as char}
    <div class="relative w-52 h-80 rounded-xl overflow-hidden">
      <img src={char.PicUrl} alt={char.Name} class="object-cover w-full h-full"/>
      <p class="absolute w-full font-bold py-2.5 bottom-0 inset-x-0 bg-indigo-600 text-white text-xs text-center leading-4">{char.Name}
        <Modal><Content char={char}/></Modal> 
      </p>      
    </div>
    {/each}

  </div>

  {/if}


</div>
</main>