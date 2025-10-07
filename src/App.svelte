<script>
  //tailwind css impelemnt - https://codepen.io/resf/pen/abRqevr 
  import Upload from './user_upload.svelte';
  import GettingStarted from './info.svelte';
  import Settings from './user_settings.svelte';
  import Quiz from './seasonsq.svelte';
  //import SeasonSelector from './SeasonSelector.svelte';

  let currentPage = 'home';

  function navigate(page) {
    currentPage = page;
  }

  

  let menuOpen = false;
  let showQuiz = false;

  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  function triggerUpload() {
    document.getElementById('uploadInput')?.click();
    menuOpen = false;
  }

  function triggerQuiz() {
    showQuiz = true;
    menuOpen = false;
  }

  function modifySeason() {
    alert('Modify Season clicked');
    menuOpen = false;
  }
  
</script>

<!-- Hamburger Button -->
<div class="fixed top-4 left-4 z-50">
  <button on:click={toggleMenu} class="p-2 bg-gray-800 text-white rounded-full text-xl">
    {menuOpen ? '×' : '☰'}
  </button>
</div>

<!-- Fullscreen Menu -->
{#if menuOpen}
  <div class="fixed inset-0 bg-black bg-opacity-90 z-40 flex flex-col items-center justify-center space-y-6 text-white text-2xl">
    <button on:click={triggerUpload} class="hover:text-indigo-300 transition">Upload PNG</button>
    <button on:click={triggerQuiz} class="hover:text-indigo-300 transition">Seasonal Quiz</button>
    <button on:click={modifySeason} class="hover:text-indigo-300 transition">Modify Season</button>
  </div>
{/if}

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

{#if showQuiz}
  <Quiz on:close={() => showQuiz = false} />
{/if}

<main>


  
  

  

</main>

<style>

</style>
