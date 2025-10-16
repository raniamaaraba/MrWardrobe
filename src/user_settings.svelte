<!-- user_settings.svelte - complete updated version -->
<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  
  let file;
  let error = '';
  let previewUrl = '';
  let fileInput;
  let userName = '';
  let successMessage = '';
  
  // Get existing users from localStorage or use defaults
  let users = JSON.parse(localStorage.getItem('users') || '[]');
  if (users.length === 0) {
    // Add default users if none exist
    users = [
      { name: 'Meredith', image: '/photos/meredith.png', isDefault: true },
      { name: 'Rania', image: '/photos/rania.png', isDefault: true }
    ];
  }

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
    
    // Create preview
    const reader = new FileReader();
    reader.onload = (e) => {
      previewUrl = e.target.result;
    };
    reader.readAsDataURL(file);
  }
  
  function saveNewUser() {
    if (!file || !userName.trim()) {
      error = 'Please upload an image and enter a name.';
      return;
    }
    
    // Save the image data and user info
    const reader = new FileReader();
    reader.onload = () => {
      const newUser = {
        name: userName.trim(),
        image: reader.result,
        isDefault: false
      };
      
      // Add to users array
      users.push(newUser);
      
      // Save to localStorage
      localStorage.setItem('users', JSON.stringify(users));
      
      // Clear form
      file = null;
      previewUrl = '';
      userName = '';
      successMessage = `User "${newUser.name}" added successfully!`;
      error = '';
      
      // Notify parent component about new user
      dispatch('userAdded', newUser.name);
      
      // Clear success message after 3 seconds
      setTimeout(() => {
        successMessage = '';
      }, 3000);
    };
    reader.readAsDataURL(file);
  }
  
  function deleteUser(index) {
    if (users[index].isDefault) {
      error = "Can't delete default users.";
      return;
    }
    
    const deletedName = users[index].name;
    users.splice(index, 1);
    localStorage.setItem('users', JSON.stringify(users));
    successMessage = `User "${deletedName}" deleted.`;
  }
</script>

<main>
  <h1>Settings</h1>

  <h2>Upload New User:</h2>
  
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

    {#if previewUrl}
      <img src={previewUrl} alt="Preview" class="mt-4 w-32 h-32 object-cover rounded shadow mx-auto" />
    {/if}
  </div>

  <p>
    Enter a name for the user:
    <input 
      type="text" 
      bind:value={userName}
      class="w-full px-2 py-1 bg-white text-gray-900 border-2 border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-purple-500"
      placeholder="Enter name..."
    >
  </p>

  <button 
    on:click={saveNewUser}
    type="button" 
    class="text-white bg-gradient-to-r from-purple-500 via-purple-600 to-purple-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-purple-300 dark:focus:ring-purple-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2">
    Submit
  </button>

  {#if error}
    <p class="mt-2 text-red-600 text-sm">{error}</p>
  {/if}
  
  {#if successMessage}
    <p class="mt-2 text-green-400 text-sm">{successMessage}</p>
  {/if}

  <h2 class="mt-8">Existing Users:</h2>
  <div class="space-y-2">
    {#each users as user, i}
      <div class="flex items-center justify-between bg-gray-800 p-3 rounded">
        <span class="text-white">{user.name}</span>
        {#if !user.isDefault}
          <button 
            on:click={() => deleteUser(i)}
            class="px-3 py-1 bg-red-600 text-white rounded text-sm hover:bg-red-700">
            Delete
          </button>
        {:else}
          <span class="text-gray-500 text-sm">Default</span>
        {/if}
      </div>
    {/each}
  </div>
</main>

<style>
  h1 {
    align-self: center;
  }
  h2 {
    align-self: self-start;
  }
</style>