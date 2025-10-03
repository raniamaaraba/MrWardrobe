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

  let currentSeason = '';
  const seasons = [
    { name: 'Spring', color: 'bg-pink-300 hover:bg-pink-400' },
    { name: 'Summer', color: 'bg-yellow-400 hover:bg-yellow-500' },
    { name: 'Autumn', color: 'bg-orange-600 hover:bg-orange-700' },
    { name: 'Winter', color: 'bg-blue-400 hover:bg-blue-500' }
  ];
</script>


<main>
    <h1>
        Settings
    </h1>

    
    <h2>
        Upload New User:
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


    

    <h2>
        Modify Your Season:
    </h2>

    <div class="flex flex-wrap justify-center gap-4 mt-8">
        {#each seasons as season}
            <button
            on:click={() => currentSeason = season.name}
            class={`px-6 py-3 rounded text-white transition
                ${season.color}
                ${currentSeason === season.name ? 'ring-4 ring-offset-2 ring-white' : ''}`}
            >
            {season.name}
            </button>
        {/each}
        </div>



</main>

<style>
    h1{
        align-self: center;
    }

    h2{
        align-self: self-start;
    }
</style>