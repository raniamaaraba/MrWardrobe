<!-- outfit_builder.svelte -->
<script>
  import { onMount } from 'svelte';
  
  export let selectedUser = 'Meredith';
  export let userSeason = '';
  
  // Color to season mapping
  const colorToSeasonMap = {
    // Neutrals
    'Black': ['Deep Winter', 'Bright Winter'],
    'Charcoal': ['Soft Summer', 'Cool Summer', 'Deep Winter'],
    'Grey': ['Soft Summer', 'Cool Summer'],
    'White': ['Bright Winter', 'Light Spring'],
    'Ivory': ['Light Spring', 'Warm Autumn'],
    'Nude': ['Bright Winter', 'Warm Autumn'],
    'Chiffon': ['Soft Summer', 'Light Spring'],
    'Beige': ['Light Spring', 'Warm Autumn'],
    'Tan': ['Warm Autumn'],
    'Espresso': ['Warm Autumn', 'Deep Winter'],
    
    // Blues
    'Light Blue': ['Light Spring', 'Soft Summer', 'Cool Summer'],
    'Dark Blue': ['Deep Winter', 'Cool Summer'],
    'Denim': ['Light Spring'],
    'Soft Navy': ['Soft Summer'],
    'Navy': ['Cool Summer', 'Deep Winter'],
    'Royal Blue': ['Deep Winter', 'Bright Winter'],
    'Cornflower': ['Cool Summer'],
    'Tiffany Blue': ['Warm Autumn'],
    'Jelly': ['Cool Summer'],
    'Midnight': ['Bright Winter', 'Deep Winter'],
    'Blue': ['Bright Winter'],
    
    // Reds & Pinks
    'Pink': ['Light Spring', 'Soft Summer'],
    'Blush Pink': ['Soft Summer'],
    'Red': ['Deep Winter', 'Bright Winter', 'Warm Autumn'],
    'Soft Red': ['Light Spring'],
    'True Red': ['Deep Winter', 'Bright Winter'],
    'American Rose': ['Cool Summer'],
    'Strawberry': ['Soft Summer'],
    'Crimson': ['Warm Autumn', 'Deep Winter'],
    'Cotton Candy': ['Cool Summer', 'Light Spring'],
    'Burgundy': ['Deep Winter', 'Warm Autumn'],
    
    // Yellows & Oranges
    'Light Yellow': ['Light Spring'],
    'Yellow': ['Light Spring', 'Bright Winter'],
    'Honey Yellow': ['Light Spring'],
    'Lemon': ['Bright Winter'],
    'Sunflower': ['Deep Winter'],
    'Light Orange': ['Warm Autumn', 'Light Spring'],
    'Dark Orange': ['Warm Autumn'],
    'Butterscotch': ['Warm Autumn'],
    'Salmon': ['Warm Autumn', 'Soft Summer'],
    'Coral': ['Warm Autumn', 'Light Spring'],
    
    // Greens
    'Light Green': ['Light Spring', 'Cool Summer'],
    'Dark Green': ['Deep Winter', 'Warm Autumn'],
    'Green': ['Light Spring', 'Cool Summer'],
    'Soft Olive': ['Light Spring'],
    'Seafoam': ['Soft Summer'],
    'Basil': ['Warm Autumn'],
    'Asparagus': ['Cool Summer'],
    'Jungle Green': ['Deep Winter'],
    'Jade': ['Bright Winter'],
    
    // Purples
    'Light Purple': ['Soft Summer', 'Cool Summer'],
    'Dark Purple': ['Deep Winter', 'Bright Winter'],
    'Lavender': ['Light Spring'],
    'Amethyst': ['Deep Winter'],
    'Grape': ['Bright Winter'],
    'Violet': ['Cool Summer'],
    'Mauve': ['Soft Summer']
  };
  
  let wardrobe = [];
  let tops = [];
  let bottoms = [];
  let currentTopIndex = 0;
  let currentBottomIndex = 0;
  let matchPercentage = 0;
  
    // Get users from localStorage to build image map
    let users = JSON.parse(localStorage.getItem('users') || '[]');
    if (users.length === 0) {
    users = [
        { name: 'Meredith', image: '/photos/meredith.png' },
        { name: 'Rania', image: '/photos/rania.png' }
    ];
    }

    const userImages = users.reduce((acc, user) => {
    acc[user.name] = user.image;
    return acc;
    }, {});
  const localItems = [
    { imageData: '/photos/topm.png', source: 'local', itemType: 'Top', colorTag: 'Dark Blue' },
    { imageData: '/photos/topm1.png', source: 'local', itemType: 'Top', colorTag: 'Dark Purple' },
    { imageData: '/photos/topm2.png', source: 'local', itemType: 'Top', colorTag: 'Espresso' },
    { imageData: '/photos/topm3.png', source: 'local', itemType: 'Top', colorTag: 'Dark Blue' },
    { imageData: '/photos/topm4.png', source: 'local', itemType: 'Top', colorTag: 'Ivory' },
    { imageData: '/photos/topm5.png', source: 'local', itemType: 'Top', colorTag: 'Ivory' },
    { imageData: '/photos/topm6.png', source: 'local', itemType: 'Top', colorTag: 'Red' },
    { imageData: '/photos/topm7.png', source: 'local', itemType: 'Top', colorTag: 'Grey' },
    { imageData: '/photos/topm8.png', source: 'local', itemType: 'Top', colorTag: 'Yellow' },
    { imageData: '/photos/topm9.png', source: 'local', itemType: 'Top', colorTag: 'Dark Blue' },
    { imageData: '/photos/topm10.png', source: 'local', itemType: 'Top', colorTag: 'Grey' },
    { imageData: '/photos/topm12.png', source: 'local', itemType: 'Top', colorTag: 'Grey' },
    { imageData: '/photos/topm13.png', source: 'local', itemType: 'Top', colorTag: 'Light Blue' },
    { imageData: '/photos/topm14.png', source: 'local', itemType: 'Top', colorTag: 'Grey' },
    { imageData: '/photos/topm15.png', source: 'local', itemType: 'Top', colorTag: 'Grey' },

    { imageData: '/photos/Bottom1.png', source: 'local', itemType: 'Bottom', colorTag: 'Green' },
    { imageData: '/photos/Bottom2.png', source: 'local', itemType: 'Bottom', colorTag: 'Brown' },
    { imageData: '/photos/Bottom3.png', source: 'local', itemType: 'Bottom', colorTag: 'Black' },
    { imageData: '/photos/Bottom4.png', source: 'local', itemType: 'Bottom', colorTag: 'grey' },
    { imageData: '/photos/Bottom6.png', source: 'local', itemType: 'Bottom', colorTag: 'black' },
    { imageData: '/photos/Bottom7.png', source: 'local', itemType: 'Bottom', colorTag: 'Dark blue' },
    { imageData: '/photos/Bottom8.png', source: 'local', itemType: 'Bottom', colorTag: 'Black' },
    { imageData: '/photos/Bottom9.png', source: 'local', itemType: 'Bottom', colorTag: 'Black' },
    { imageData: '/photos/Bottom10.png', source: 'local', itemType: 'Bottom', colorTag: 'Ivory' },
    { imageData: '/photos/Bottom11.png', source: 'local', itemType: 'Bottom', colorTag: 'Green' },
    { imageData: '/photos/Bottom12.png', source: 'local', itemType: 'Bottom', colorTag: 'Nude' },
    { imageData: '/photos/Bottom13.png', source: 'local', itemType: 'Bottom', colorTag: 'black' },
    { imageData: '/photos/Bottom14.png', source: 'local', itemType: 'Bottom', colorTag: 'Light Blue' },
    { imageData: '/photos/Bottom15.png', source: 'local', itemType: 'Bottom', colorTag: 'Nude' },



    { imageData: '/photos/skirt1.png', source: 'local', itemType: 'Bottom', colorTag: 'Light Blue' },
    { imageData: '/photos/skirt2.png', source: 'local', itemType: 'Bottom', colorTag: 'Light Yellow' },
    { imageData: '/photos/dress1.png', source: 'local', itemType: 'Dress', colorTag: 'Light Blue' },
    { imageData: '/photos/pants.png', source: 'local', itemType: 'Bottom', colorTag: 'Black' },
    { imageData: '/photos/sweater1.png', source: 'local', itemType: 'Top', colorTag: 'Pink' }
  ];
  
  onMount(() => {
    const stored = localStorage.getItem('wardrobe');
    const uploadedItems = stored ? JSON.parse(stored) : [];
    wardrobe = [...localItems, ...uploadedItems];
    
    tops = wardrobe.filter(item => item.itemType === 'Top');
    bottoms = wardrobe.filter(item => item.itemType === 'Bottom');
    
    if (tops.length === 0) {
      tops = [{ imageData: null, colorTag: 'None', itemType: 'Top' }];
    }
    if (bottoms.length === 0) {
      bottoms = [{ imageData: null, colorTag: 'None', itemType: 'Bottom' }];
    }
    
    calculateMatch();
  });
  
  function nextTop() {
    currentTopIndex = (currentTopIndex + 1) % tops.length;
    calculateMatch();
  }
  
  function prevTop() {
    currentTopIndex = (currentTopIndex - 1 + tops.length) % tops.length;
    calculateMatch();
  }
  
  function nextBottom() {
    currentBottomIndex = (currentBottomIndex + 1) % bottoms.length;
    calculateMatch();
  }
  
  function prevBottom() {
    currentBottomIndex = (currentBottomIndex - 1 + bottoms.length) % bottoms.length;
    calculateMatch();
  }
  
  function calculateMatch() {
    if (!userSeason || tops.length === 0 || bottoms.length === 0) {
      matchPercentage = 0;
      return;
    }
    
    const topColor = tops[currentTopIndex]?.colorTag;
    const bottomColor = bottoms[currentBottomIndex]?.colorTag;
    
    let score = 0;
    let maxScore = 2;
    
    if (topColor && colorToSeasonMap[topColor]) {
      if (colorToSeasonMap[topColor].includes(userSeason)) {
        score += 1;
      } else if (colorToSeasonMap[topColor].some(season => 
        season.split(' ')[1] === userSeason.split(' ')[1])) {
        score += 0.5;
      }
    }
    
    if (bottomColor && colorToSeasonMap[bottomColor]) {
      if (colorToSeasonMap[bottomColor].includes(userSeason)) {
        score += 1;
      } else if (colorToSeasonMap[bottomColor].some(season => 
        season.split(' ')[1] === userSeason.split(' ')[1])) {
        score += 0.5;
      }
    }
    
    matchPercentage = Math.round((score / maxScore) * 100);
  }
  
  function getMatchColor() {
    if (matchPercentage >= 80) return 'text-green-400';
    if (matchPercentage >= 50) return 'text-yellow-400';
    return 'text-red-400';
  }
</script>

<div class="outfit-builder max-w-4xl mx-auto">
  <div class="text-center mb-6">
    <h2 class="text-2xl font-bold text-white mb-2">Try On Outfits</h2>
    {#if userSeason}
      <p class="text-indigo-400">Your Season: {userSeason}</p>
    {:else}
      <p class="text-gray-400">Take the quiz to see your seasonal match!</p>
    {/if}
  </div>
  
  <div class="relative mx-auto" style="width: 400px; height: 600px;">
    <img 
      src={userImages[selectedUser]} 
      alt={selectedUser}
      class="absolute inset-0 w-full h-full object-contain z-10"
    />
    
<!-- Update the image containers in outfit_builder.svelte -->
    <!-- Replace the existing image overlay sections in outfit_builder.svelte -->

    {#if tops[currentTopIndex]?.imageData}
    <div class="absolute z-20 flex items-start justify-center" style="
        top: 155px; 
        left: 47%; 
        transform: translateX(-50%); 
        width: 640px;
        height: 170px;
        overflow: hidden;
    ">
        <img 
        src={tops[currentTopIndex].imageData} 
        alt="Top"
        class="w-full object-contain object-top"
        style="max-height: 100%;"
        />
    </div>
    {/if}

    {#if bottoms[currentBottomIndex]?.imageData}
    <div class="absolute z-20 flex items-start justify-center" style="
        top: 290px; 
        left: 47%; 
        transform: translateX(-50%); 
        width: 290px;
        height: 240px;
        overflow: hidden;
    ">
        <img 
        src={bottoms[currentBottomIndex].imageData} 
        alt="Bottom"
        class="w-full object-contain object-top"
        style="max-height: 100%;"
        />
    </div>
    {/if}
    <button 
      on:click={prevTop}
      class="absolute left-2 top-1/3 z-30 text-red-500 hover:text-red-400 text-3xl font-bold bg-black/30 rounded-full w-10 h-10 flex items-center justify-center"
      style="transform: translateY(-50%);"
    >
      ‹
    </button>
    
    <button 
      on:click={nextTop}
      class="absolute right-2 top-1/3 z-30 text-red-500 hover:text-red-400 text-3xl font-bold bg-black/30 rounded-full w-10 h-10 flex items-center justify-center"
      style="transform: translateY(-50%);"
    >
      ›
    </button>
    
    <button 
      on:click={prevBottom}
      class="absolute left-2 top-2/3 z-30 text-red-500 hover:text-red-400 text-3xl font-bold bg-black/30 rounded-full w-10 h-10 flex items-center justify-center"
      style="transform: translateY(-50%);"
    >
      ‹
    </button>
    
    <button 
      on:click={nextBottom}
      class="absolute right-2 top-2/3 z-30 text-red-500 hover:text-red-400 text-3xl font-bold bg-black/30 rounded-full w-10 h-10 flex items-center justify-center"
      style="transform: translateY(-50%);"
    >
      ›
    </button>
  </div>
  
  <div class="text-center mt-8">
    <div class="text-4xl font-bold {getMatchColor()}">
      {matchPercentage}% Match
    </div>
    <p class="text-gray-400 mt-2">
      {#if matchPercentage >= 80}
        Perfect outfit for your {userSeason} palette!
      {:else if matchPercentage >= 50}
        Good combination, but could be better for {userSeason}.
      {:else}
        Consider different colors for your {userSeason} palette.
      {/if}
    </p>
  </div>
  
  <div class="grid grid-cols-2 gap-4 mt-6">
    <div class="bg-gray-800 p-4 rounded">
      <h3 class="font-bold text-white mb-2">Top</h3>
      {#if tops[currentTopIndex]}
        <p class="text-sm text-gray-300">Color: {tops[currentTopIndex].colorTag}</p>
        <p class="text-xs text-gray-400 mt-1">
          {currentTopIndex + 1} of {tops.length}
        </p>
      {/if}
    </div>
    
    <div class="bg-gray-800 p-4 rounded">
      <h3 class="font-bold text-white mb-2">Bottom</h3>
      {#if bottoms[currentBottomIndex]}
        <p class="text-sm text-gray-300">Color: {bottoms[currentBottomIndex].colorTag}</p>
        <p class="text-xs text-gray-400 mt-1">
          {currentBottomIndex + 1} of {bottoms.length}
        </p>
      {/if}
    </div>
  </div>
</div>