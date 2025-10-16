<!-- modify_season.svelte -->
<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  
  export let currentSeason = '';
  
  let showQuiz = false;
  let manualSelection = false;
  
  const seasons = [
    'Light Spring',
    'Soft Summer', 
    'Cool Summer',
    'Warm Autumn',
    'Deep Winter',
    'Bright Winter'
  ];
  
  function selectSeason(season) {
    currentSeason = season;
    // Save to localStorage for persistence
    localStorage.setItem('userSeason', season);
    dispatch('seasonChanged', season);
    manualSelection = false;
  }
  
  function startQuiz() {
    dispatch('startQuiz');
  }
</script>

<div class="fixed inset-0 bg-black/60 backdrop-blur-sm flex items-center justify-center z-50">
  <div class="bg-white rounded-xl shadow-2xl p-6 w-full max-w-md animate-fade-in relative">
    <button
      on:click={() => dispatch('close')}
      class="absolute top-2 right-2 text-gray-500 hover:text-gray-700 text-xl font-bold"
    >
      ×
    </button>

    <h2 class="text-2xl font-bold text-indigo-700 mb-4">Modify Your Season</h2>
    
    <div class="mb-6 p-4 bg-gray-100 rounded-lg">
      <p class="text-sm text-gray-600">Current Season:</p>
      <p class="text-xl font-bold text-indigo-600">{currentSeason || 'Not set'}</p>
    </div>

    <div class="space-y-4">
      <button
        on:click={startQuiz}
        class="w-full px-4 py-3 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition font-medium"
      >
        Retake Season Quiz
      </button>
      
      <button
        on:click={() => manualSelection = !manualSelection}
        class="w-full px-4 py-3 bg-gray-600 text-white rounded-lg hover:bg-gray-700 transition font-medium"
      >
        {manualSelection ? 'Cancel' : 'Manually Select Season'}
      </button>
    </div>

    {#if manualSelection}
      <div class="mt-4 space-y-2">
        <p class="text-sm text-gray-600 mb-2">Choose your season:</p>
        <div class="grid grid-cols-2 gap-2">
          {#each seasons as season}
            <button
              on:click={() => selectSeason(season)}
              class="px-3 py-2 text-sm rounded-lg transition
                {season === currentSeason 
                  ? 'bg-indigo-600 text-white' 
                  : 'bg-gray-200 text-gray-800 hover:bg-gray-300'}"
            >
              {season}
            </button>
          {/each}
        </div>
      </div>
    {/if}
    
    <div class="mt-6 text-xs text-gray-500 text-center">
      Your season determines which colors look best on you
    </div>
  </div>
</div>

<style>
  @keyframes fade-in {
    from { opacity: 0; transform: scale(0.95); }
    to { opacity: 1; transform: scale(1); }
  }
  .animate-fade-in {
    animation: fade-in 0.3s ease-out;
  }
</style>