<script>
  let openIndex = null;

  const questions = [
    {
      title: 'What is Mr Wardobe?',
      answer: "With the help of your input, Mr Wardrobe customises and makes planning outfits easy! Upload an image of yourself, take a quick quiz about your Seasonal Colors, and we will match you with perfect outfits! Don't like our choice? No problem! Use the arrows to switch your selected item and see the probability if the outfit works!"
    },
    {
      title: 'What happens if I get a new piece of clothing?',
      answer: "No worries! Head over to the 'Upload' tab and add in your new item! Our system will automatically render and add the image to your closet."
    },
    {
      title: 'What if this is not me?',
      answer: 'In Settings, you can change any of your original settings to Switch Users, Change your Season, and other quality of life improvements.'
    },
    {
      title: "What do you mean by 'Season'?",
      answer: 'Based on your skin tone, eye color, under-tones, vein color, and many more genetic features, your Season is determined. The Season result then allow us to determine which colors look best on your skin tone and reccomend outfits you will love!'
    }
  ];

  function toggle(index) {
    openIndex = openIndex === index ? null : index;
  }
</script>


<main class="max-w-xl mx-auto mt-8 space-y-4">
    <h1>
        How to Get Started
    </h1>

    <div class="max-w-xl mx-auto mt-8 space-y-4">
        {#each questions as q, i}
            <div class="border-b pb-2">
                <div class="flex items-center justify-between cursor-pointer" on:click={() => toggle(i)}>
                    <span class="text-base font-medium text-white-800">{q.title}</span>
                    <span class="text-xl text-gray-500 transform transition-transform duration-200 {openIndex === i ? 'rotate-180' : ''}">
                    ↓
                    </span>
                </div>

                {#if openIndex === i}
                    <div class="mt-2 text-white-700 text-sm">
                    {q.answer}
                    </div>
                {/if}
            </div>
        {/each}
    </div>

    
</main>





