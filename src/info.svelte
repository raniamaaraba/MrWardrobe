<!-- info.svelte - fully responsive layout -->
<script>
  export let selectedUser = 'Meredith';
  export let userImage = '/photos/meredith.png';
  export let userSeason = '';
</script>

<main class="max-w-6xl mx-auto mt-8 px-4 sm:px-6 lg:px-8 flex flex-col items-center text-center">
  <h1 
    class="text-2xl sm:text-3xl md:text-4xl font-bold text-white mb-10 leading-tight text-center break-words whitespace-normal">
    Getting Started with Mr&nbsp;Wardrobe
  </h1>


  <!--user display -->
  <section class="flex flex-col items-center justify-center mb-16 w-full">
    <div class="flex flex-col items-center text-center">
      <img 
        src={userImage} 
        alt={selectedUser}
        class="w-56 h-56 sm:w-64 sm:h-64 md:w-80 md:h-80 object-contain rounded-xl shadow-lg mb-6 transition-all duration-300"
      />
      <p class="text-white font-bold text-lg sm:text-xl">Current User: {selectedUser}</p>
      {#if userSeason}
        <p class="text-indigo-400 mt-2 text-base sm:text-lg">Season: {userSeason}</p>
      {:else}
        <p class="text-gray-400 mt-2 text-base sm:text-lg">No season selected - Take the quiz!</p>
      {/if}
    </div>
  </section>

  <!-- starting guide -->
  <section class="w-full grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-10 mb-10 px-4 sm:px-6">
    <div class="flex flex-col items-center">
      <div class="text-4xl sm:text-5xl font-bold text-purple-500 mb-2">1</div>
      <h3 class="font-bold text-white text-xl sm:text-2xl mb-1">Select User</h3>
      <p class="text-gray-400 text-base sm:text-lg max-w-xs">Choose or add your profile</p>
    </div>

    <div class="flex flex-col items-center">
      <div class="text-4xl sm:text-5xl font-bold text-purple-500 mb-2">2</div>
      <h3 class="font-bold text-white text-xl sm:text-2xl mb-1">Take Quiz</h3>
      <p class="text-gray-400 text-base sm:text-lg max-w-xs">Discover your season colors</p>
    </div>

    <div class="flex flex-col items-center">
      <div class="text-4xl sm:text-5xl font-bold text-purple-500 mb-2">3</div>
      <h3 class="font-bold text-white text-xl sm:text-2xl mb-1">Try Outfits</h3>
      <p class="text-gray-400 text-base sm:text-lg max-w-xs">Get personalized matches</p>
    </div>
  </section>
</main>
