<script>
  let file;
  let error = '';
  let previewUrl = '';
  let fileInput;
  let showQuiz = false;
  let currentQuestion = 0;
  let selectedAnswers = {};
  let showResults = false;
  let matchedSeason = '';

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

</script>






<main>
    

    
    <h1>
        Settings
    </h1>

    
    <h2>
        Upload New User:
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

    <p>
        Enter a name for the user:
        <input type="text">
    </p>
    
    <button type="button" class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"> 
      Submit
    </button>

</main>
<style>
    h1{
        align-self: center;
    }

    h2{
        align-self: self-start;
    }
</style>