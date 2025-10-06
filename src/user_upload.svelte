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
    <div class="p-6 max-w-md mx-auto bg-white rounded shadow">
        <button on:click={triggerUpload} class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700 transition">
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
    <button class="border-purple-200 text-purple-600 hover:border-transparent hover:bg-purple-600 hover:text-white active:bg-purple-700 ...">
      Submit
    </button>
</main>