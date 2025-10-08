<script>
  //tailwind css impelemnt - https://codepen.io/resf/pen/abRqevr 
  import Upload from './user_upload.svelte';
  import GettingStarted from './info.svelte';
  import Settings from './user_settings.svelte';
  import Quiz from './seasonsq.svelte';
  //import SeasonSelector from './SeasonSelector.svelte';

  let menuOpen = false;
  let showQuiz = false;

  let currentPage = 'home';

  function navigate(page) {
    currentPage = page;
  }

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

  let selectedName = 'Meredith';

  function toggleName() {
    selectedName = selectedName === 'Meredith' ? 'Rania' : 'Meredith';
  }

  const imageMap = {
    Meredith: '/photos/meredith.png',
    Rania: '/photos/rania.png'
  };
  
</script>

<!--hamburger -->
<div class="fixed top-4 left-4 z-50">
  <button on:click={toggleMenu} class="p-2 bg-gray-800 text-white rounded-full text-xl">
    {menuOpen ? '×' : '☰'}
  </button>
</div>

<!--dropdown menu-->
{#if menuOpen}
  <div class="fixed inset-0 bg-black bg-opacity-90 z-40 flex flex-col items-center justify-center space-y-6 text-white text-2xl">
    <button on:click={triggerUpload} class="hover:text-indigo-300 transition">Upload PNG</button>
    <button on:click={triggerQuiz} class="hover:text-indigo-300 transition">Seasonal Quiz</button>
    <button on:click={modifySeason} class="hover:text-indigo-300 transition">Modify Season</button>
  </div>
{/if}



{#if showQuiz}
  <Quiz on:close={() => showQuiz = false} />
{/if}





<main>
  <h1>
    Mr Wardrobe
  </h1>

  <!-- button design logic: https://flowbite.com/docs/components/buttons/#gradient-monochrome-->

  <!-- button inside main so no white border-->
  <button on:click= {() => navigate('settings')} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
    Settings
  </button>
  <button on:click= {() => navigate('upload')} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
    Uploads
  </button>
  <button on:click= {() => navigate('getting-started')} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
    Getting Started
  </button>

  <!--switch content -->
  {#if currentPage === 'settings'}
    <Settings />
  {:else if currentPage === 'upload'}
    <Upload />
  {:else if currentPage === 'getting-started'}
    <GettingStarted />
  {/if}

  <div class="max-w-md mx-auto mt-8 space-y-4 text-center">
    <h2 class="text-white text-xl font-bold">
      You Selected:
      <button on:click={toggleName} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
        {selectedName}
      </button>
    </h2>

  <img
    src={imageMap[selectedName]}
    alt="Seasonal reference"/>
  </div>


  
  

  

</main>

<style>

</style>
