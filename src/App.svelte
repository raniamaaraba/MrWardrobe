<script>
  import Upload from './user_upload.svelte';
  import GettingStarted from './info.svelte';
  import Settings from './user_settings.svelte';

  let currentPage = 'home';

  function navigate(page) {
    currentPage = page;
  }
  
</script>

<!--buttons -->
<div class="flex justify-normal bg-gray-100">
    <button on:click={() => navigate('settings')} class="px-4 py-2 bg-red-500 text-white rounded shadow-lg hover:bg-red-600 transition">
    Settings
    </button>
    <button on:click={() => navigate('upload')} class="px-4 py-2 bg-red-500 text-white rounded shadow-lg hover:bg-red-600 transition">
      Upload
    </button>
    <button on:click={() => navigate('getting-started')} class="px-4 py-2 bg-red-500 text-white rounded shadow-lg hover:bg-red-600 transition">
      Getting Started
    </button>
  
  <!--switch content -->
  {#if currentPage === 'settings'}
    <Settings />
  {:else if currentPage === 'upload'}
    <Upload />
  {:else if currentPage === 'getting-started'}
    <GettingStarted />
  {:else}
    <h1>
      Mr Wardrobe
    </h1>
  {/if}
</div>

<main>


  
  

  

</main>

<style>

</style>
