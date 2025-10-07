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

</main>
<style>
    h1{
        align-self: center;
    }

    h2{
        align-self: self-start;
    }
</style>