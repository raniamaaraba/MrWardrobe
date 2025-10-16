<script>
  import { onMount } from 'svelte';

  let file;
  let error = '';
  let previewUrl = '';
  let fileInput;
  let selectedFile = null;

  let wardrobe = [];
  let currentIndex = 0;

  function triggerUpload() {
    fileInput.click();
  }

  function handleFileChange(event) {
    const selected = event.target.files[0];
    if (!selected) return;

    if (selected.type !== 'image/png') {
      error = 'Only PNG files are allowed.';
      selectedFile = null;
      previewUrl = '';
      return;
    }

    error = '';
    selectedFile = selected;
    previewUrl = URL.createObjectURL(selectedFile);
  }

  let selectedItem = '';
  const items = ['Top', 'Bottom', 'Dress', 'Accesory', 'Shoe'];
  let selectedItem2 = '';
  // Replace the existing items2 array with this comprehensive list
const items2 = [
  // Neutrals
  'Black',
  'Charcoal',
  'Grey',
  'White',
  'Ivory',
  'Nude',
  'Chiffon',
  'Beige',
  'Tan',
  'Espresso',
  
  // Blues
  'Light Blue',
  'Dark Blue',
  'Denim',
  'Soft Navy',
  'Navy',
  'Royal Blue',
  'Cornflower',
  'Tiffany Blue',
  'Jelly',
  'Midnight',
  'Blue',
  
  // Reds & Pinks
  'Pink',
  'Blush Pink',
  'Red',
  'Soft Red',
  'True Red',
  'American Rose',
  'Strawberry',
  'Crimson',
  'Cotton Candy',
  'Burgundy',
  
  // Yellows & Oranges
  'Light Yellow',
  'Honey Yellow',
  'Lemon',
  'Sunflower',
  'Light Orange',
  'Dark Orange',
  'Butterscotch',
  'Salmon',
  'Coral',
  
  // Greens
  'Light Green',
  'Dark Green',
  'Soft Olive',
  'Seafoam',
  'Basil',
  'Asparagus',
  'Jungle Green',
  'Jade',
  
  // Purples
  'Light Purple',
  'Dark Purple',
  'Lavender',
  'Amethyst',
  'Grape',
  'Violet',
  'Mauve'
].sort();
  //ROY G BIV

  function saveUploadedImages() {
    const uploadedOnly = wardrobe.filter(item => item.source === 'uploaded');
    localStorage.setItem('wardrobe', JSON.stringify(uploadedOnly));
  }
  //local photos
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
      { imageData: '/photos/Bottom1.png', source: 'local', itemType: 'Bottom', colorTag: 'yellow' },
      { imageData: '/photos/Bottom2.png', source: 'local', itemType: 'Bottom', colorTag: 'black' },
      { imageData: '/photos/Bottom3.png', source: 'local', itemType: 'Bottom', colorTag: 'grey' },

      { imageData: '/photos/Bottom5.png', source: 'local', itemType: 'Bottom', colorTag: 'black' },
      { imageData: '/photos/Bottom6.png', source: 'local', itemType: 'Bottom', colorTag: 'dark blue' },
      { imageData: '/photos/Bottom7.png', source: 'local', itemType: 'Bottom', colorTag: 'back' },
      { imageData: '/photos/Bottom8.png', source: 'local', itemType: 'Bottom', colorTag: 'black' },
      { imageData: '/photos/Bottom9.png', source: 'local', itemType: 'Bottom', colorTag: 'Ivory' },
      { imageData: '/photos/Bottom10.png', source: 'local', itemType: 'Bottom', colorTag: 'green' },
      { imageData: '/photos/Bottom11.png', source: 'local', itemType: 'Bottom', colorTag: 'nude' },
      { imageData: '/photos/Bottom12.png', source: 'local', itemType: 'Bottom', colorTag: 'dark green' },
      { imageData: '/photos/Bottom13.png', source: 'local', itemType: 'Bottom', colorTag: 'light blue' },
      { imageData: '/photos/Bottom14.png', source: 'local', itemType: 'Bottom', colorTag: 'nude' },
      { imageData: '/photos/Bottom15.png', source: 'local', itemType: 'Bottom', colorTag: 'light green' },

      

      { imageData: '/photos/skirt1.png', source: 'local', itemType: 'Bottom', colorTag: 'Light Blue' },
      { imageData: '/photos/skirt2.png', source: 'local', itemType: 'Bottom', colorTag: 'Light Yellow' },
      { imageData: '/photos/dress1.png', source: 'local', itemType: 'Dress', colorTag: 'Light Blue' },
      { imageData: '/photos/pants.png', source: 'local', itemType: 'Bottom', colorTag: 'Black' },
      { imageData: '/photos/sweater1.png', source: 'local', itemType: 'Top', colorTag: 'Pink' }
    ];

  //try save local storage?
  function saveImage() {
    if (!selectedFile) {
      error = 'No image selected.';
      return;
    }
    if (!selectedItem || !selectedItem2) {
      error = 'Please select both item type and color.';
      return;
    }

    const reader = new FileReader();
    reader.onload = () => {
      const imageData = reader.result;
      const newItem = {
        imageData,
        timestamp: Date.now(),
        source: 'uploaded',
        itemType: selectedItem,
        colorTag: selectedItem2
      };

      wardrobe.push(newItem);
      saveUploadedImages();
      currentIndex = wardrobe.length - 1;
      selectedFile = null;
      selectedItem = '';
      selectedItem2 = '';
      previewUrl = '';
    };
    reader.readAsDataURL(selectedFile);
  }

  function nextImage() {
    currentIndex = (currentIndex + 1) % wardrobe.length;
  }

  function prevImage() {
    currentIndex = (currentIndex - 1 + wardrobe.length) % wardrobe.length;
  }

  function deleteImage() {

    wardrobe.splice(currentIndex, 1);
    saveUploadedImages();
    currentIndex = Math.max(0, currentIndex - 1);
  }

  onMount(() => {
    const stored = localStorage.getItem('wardrobe');
    const uploadedItems = stored ? JSON.parse(stored) : [];
    wardrobe = [...localItems, ...uploadedItems];
  });

  
</script>
  


<main class="max-w-xl mx-auto mt-8 space-y-6">
  <h1 class="text-2xl font-bold text-white text-center">Upload Media</h1>

  <h2 class="text-lg font-semibold text-white">Upload New Item:</h2>

  <div>
    <button on:click={triggerUpload} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center mb-2"> 
      Upload PNG
    </button>

    <input
      type="file"
      accept=".png,image/png"
      bind:this={fileInput}
      on:change={handleFileChange}
      class="hidden"
    />

    {#if error}
      <p class="mt-2 text-red-600 text-sm">{error}</p>
    {/if}

    {#if previewUrl}
      <img src={previewUrl} alt="Preview" class="mt-4 w-32 h-32 object-cover rounded shadow mx-auto" />
    {/if}
  </div>

  <div class="max-w-sm mx-auto">
    <label class="block mb-2 font-medium text-white">Choose Item Type</label>
    <select
      bind:value={selectedItem}
      class="w-full px-4 py-2 bg-white text-gray-900 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-purple-500">
      <option value="" disabled selected>Select an Item</option>
      {#each items as item}
        <option value={item} class="text-gray-900">{item}</option>
      {/each}
    </select>

  </div>

  <div class="max-w-sm mx-auto">
    <label class="block mb-2 font-medium text-white">Choose Item Color</label>
    <select
      bind:value={selectedItem2}
      class="w-full px-4 py-2 bg-white text-gray-900 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-purple-500">
      <option value="" disabled selected>Select a Color</option>
      {#each items2 as item}
        <option value={item} class="text-gray-900">{item}</option>
      {/each}
    </select>
  </div>

  <button on:click={saveImage} class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center mb-2">
    Save to Wardrobe
  </button>
</main>

<div class="max-w-md mx-auto mt-8 space-y-4 text-center">
  <h2 class="text-xl font-bold text-indigo-400">View Your Wardrobe</h2>
</div>

{#if wardrobe.length > 0}
  <div class="max-w-md mx-auto mt-6 flex flex-col items-center space-y-4">
    <img
      src={wardrobe[currentIndex].imageData}
      alt="Wardrobe item"
      class="w-48 h-48 object-cover rounded shadow"
    />

    <div class="text-center">
      <p class="text-sm text-white"><strong>Item Type:</strong> {wardrobe[currentIndex].itemType}</p>
      <p class="text-sm text-white"><strong>Color Tag:</strong> {wardrobe[currentIndex].colorTag}</p>
    </div>

    <div class="flex space-x-4">
      <button on:click={prevImage} class="px-4 py-2 bg-gray-700 text-white rounded hover:bg-gray-600">← Prev</button>
      <button on:click={nextImage} class="px-4 py-2 bg-gray-700 text-white rounded hover:bg-gray-600">Next →</button>
    </div>

    <p class="text-sm text-gray-400">Image {currentIndex + 1} of {wardrobe.length}</p>

    <button on:click={deleteImage} class="mt-2 px-4 py-2 bg-red-600 text-white rounded hover:bg-red-700">
      Delete This Image
    </button>
  </div>
{:else}
  <p class="text-center text-gray-400 mt-6">No wardrobe images yet. Upload one to get started!</p>
{/if}
