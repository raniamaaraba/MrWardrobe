<script>
  //tailwind css impelemnt - https://codepen.io/resf/pen/abRqevr 
  import Upload from './user_upload.svelte';
  import GettingStarted from './info.svelte';
  import Settings from './user_settings.svelte';
  import Quiz from './seasonsq.svelte';
  //import SeasonSelector from './SeasonSelector.svelte';

  let showQuiz = false;

  let userSeason = '';
  let showSeasonPopup = false;

  let currentPage = 'home';

  function navigate(page) {
    currentPage = page;
  }

  function triggerQuiz() {
    showQuiz = true;
  }

  function handleSeason(event) {
    userSeason = event.detail;
    showQuiz = false;
    showSeasonPopup = true;
  }

  function showSeason() {
    if (userSeason) {
      showSeasonPopup = true;
    } else {
      alert("Please take the quiz first.");
    }
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


<!-- tailwind: https://www.codewithfaraz.com/content/528/create-html-layout-generator-tool-with-tailwind-css-js-->

<!--replace ham  -->
<div class="fixed top-0 left-0 h-full w-64 bg-gray-900 text-white p-6 space-y-6 shadow-xl z-40">
  <h2 class="text-2xl font-bold text-indigo-400 mb-6">Mr Wardrobe</h2>
  <button on:click={() => navigate('getting-started')} class="w-full bg-purple-600 hover:bg-purple-700 py-3 px-4 rounded-lg font-bold transition-transform transform hover:scale-105">
    Getting Started
  </button>
  <button on:click={triggerQuiz} class="w-full bg-purple-600 hover:bg-purple-700 py-3 px-4 rounded-lg font-bold transition-transform transform hover:scale-105">
    Seasons Quiz
  </button>
  <button on:click={() => navigate('settings')} class="w-full bg-purple-600 hover:bg-purple-700 py-3 px-4 rounded-lg font-bold transition-transform transform hover:scale-105">
    Settings
  </button>
  <hr class="border-gray-700 my-4" />
  <button on:click={() => navigate('upload')} class="w-full bg-gray-700 hover:bg-gray-600 py-2 px-4 rounded text-sm font-medium">
    Uploads
  </button>
  <button on:click={() => showSeasonPopup = true} class="w-full bg-gray-700 hover:bg-gray-600 py-2 px-4 rounded text-sm font-medium">
    Modify Season
  </button>
  <button on:click={() => navigate('app')} class="w-full bg-gray-700 hover:bg-gray-600 py-2 px-4 rounded text-sm font-medium">
    Home
  </button>
</div>


<!--show the correct sabed season-->
{#if showQuiz}
  <Quiz on:close={() => showQuiz = false} on:season={(e) => {userSeason = e.detail;}}/>
  {/if}


<main>
  <!-- button design logic: https://flowbite.com/docs/components/buttons/#gradient-monochrome-->

  <!--switch content -->
  {#if currentPage === 'settings'}
    <Settings />
  {:else if currentPage === 'upload'}
    <Upload />
  {:else if currentPage === 'getting-started'}
    <GettingStarted />
  {:else}


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

  {/if}

  {#if showSeasonPopup}
    <div class="fixed inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50">
      <div class="bg-white rounded-xl shadow-2xl p-6 w-full max-w-sm text-center animate-fade-in relative">
        <button
          on:click={() => showSeasonPopup = false}
          class="absolute top-2 right-2 text-gray-500 hover:text-gray-700 text-sm font-bold"
        >
          ×
        </button>

        <h2 class="text-xl font-bold text-indigo-700 mb-2">Your Season</h2>
        <p class="text-gray-800 font-medium">{userSeason || 'No season selected yet.'}</p>
      </div>
    </div>
  {/if}
</main>

<style>

</style>
