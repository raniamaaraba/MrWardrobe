<script>
  let file;
  let error = '';
  let previewUrl = '';
  let fileInput;

  function triggerUpload() {
    fileInput.click();
  }

  function handleFileChange(event) {
    const selected = event.target.files[0];
    if (!selected) return;

    if (selected.type !== 'image/png') {
      error = 'Only PNG files are allowed.';
      file = null;
      previewUrl = '';
      return;
    }

    error = '';
    file = selected;
    previewUrl = URL.createObjectURL(file);
  }

  let selectedItem = '';
  const items = ['Top', 'Bottom', 'Dress', 'Accesory', 'Shoe'];

</script>

<main>
    <h1>
        Upload Media
    </h1>

    <h2>
        Upload New Item:
    </h2>
    <!-- stil need to add db to save user upload-->
    <div>
        <button on:click={triggerUpload} type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"> 
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

    </div>

    <div class="max-w-sm mx-auto mt-8">
        Choose Item type
    <select
        id="items"
        bind:value={selectedItem}
        class="w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
        <option value="" disabled selected>Select an Item</option>
        {#each items as item}
        <option value={item}>{item}</option>
        {/each}
    </select>
    </div>
    <button type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"> 
      Submit
    </button>
</main>