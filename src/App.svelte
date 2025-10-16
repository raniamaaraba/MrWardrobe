<script>
  //tailwind css impelemnt - https://codepen.io/resf/pen/abRqevr 
  import { onMount } from 'svelte';
  import Upload from './user_upload.svelte';
  import GettingStarted from './info.svelte';
  import Settings from './user_settings.svelte';
  import Quiz from './seasonsq.svelte';
  import OutfitBuilder from './outfit_builder.svelte';
  import ModifySeason from './modify_season.svelte';
  //import SeasonSelector from './SeasonSelector.svelte';

  let showQuiz = false;
  let userSeason = '';
  let showSeasonPopup = false;
  let showModifySeason = false;
  let currentPage = 'home';

  // Get users from localStorage or use defaults
  let users = JSON.parse(localStorage.getItem('users') || '[]');
  if (users.length === 0) {
    users = [
      { name: 'Meredith', image: '/photos/meredith.png' },
      { name: 'Rania', image: '/photos/rania.png' }
    ];
  }
  
  let selectedUserIndex = 0;
  $: selectedName = users[selectedUserIndex]?.name || 'Meredith';
  $: imageMap = users.reduce((acc, user) => {
    acc[user.name] = user.image;
    return acc;
  }, {});
  
  onMount(() => {
    const savedSeason = localStorage.getItem('userSeason');
    if (savedSeason) {
      userSeason = savedSeason;
    }
  });

  function navigate(page) {
    currentPage = page;
  }

  function triggerQuiz() {
    showQuiz = true;
  }

  function handleSeason(event) {
    userSeason = event.detail;
    localStorage.setItem('userSeason', userSeason);
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

  function toggleName() {
    selectedUserIndex = (selectedUserIndex + 1) % users.length;
  }
  
  function handleUserAdded(event) {
    // Reload users when a new one is added
    users = JSON.parse(localStorage.getItem('users') || '[]');
  }

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
  <button on:click={() => showModifySeason = true} class="w-full bg-gray-700 hover:bg-gray-600 py-2 px-4 rounded text-sm font-medium">
    Modify Season
  </button>
  <button on:click={() => navigate('home')} class="w-full bg-gray-700 hover:bg-gray-600 py-2 px-4 rounded text-sm font-medium">
    Home
  </button>
</div>


<!--show the correct saved season-->
{#if showQuiz}
  <Quiz on:close={() => showQuiz = false} on:season={handleSeason}/>
{/if}

{#if showModifySeason}
  <ModifySeason 
    currentSeason={userSeason}
    on:close={() => showModifySeason = false}
    on:seasonChanged={(e) => {
      userSeason = e.detail;
      showModifySeason = false;
    }}
    on:startQuiz={() => {
      showModifySeason = false;
      triggerQuiz();
    }}
  />
{/if}


<main>
  <!-- Add user selector at top of main content -->
  {#if currentPage !== 'settings' && currentPage !== 'upload'}
    <div class="text-center mb-6">
      <h2 class="text-white text-xl font-bold mb-2">
        Active User:
        <button on:click={toggleName} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
          {selectedName}
        </button>
      </h2>
    </div>
  {/if}

  <!-- button design logic: https://flowbite.com/docs/components/buttons/#gradient-monochrome-->

  <!--switch content -->
  {#if currentPage === 'settings'}
    <Settings on:userAdded={handleUserAdded} />
  {:else if currentPage === 'upload'}
    <Upload />
  {:else if currentPage === 'getting-started'}
    <GettingStarted selectedUser={selectedName} userImage={imageMap[selectedName]} {userSeason} />
  {:else}
    <OutfitBuilder selectedUser={selectedName} {userSeason} />
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