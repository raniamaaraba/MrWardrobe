<!-- https://30somethingurbangirl.com/free-quiz-what-is-your-seasonal-color/-->
<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  let currentQuestion = 0;
  let selectedAnswers = {};
  let showResults = false;
  let matchedSeason = '';

  const quiz = [
    { question: 'What is your natural hair?', options: ['Light: Golden or White Blonde', 'Warm: Strawberry Blonde, Red, or Reddish Brown', 'Soft: Medium to Deep Ash Blonde', 'Cool: Deep Ash Blonde or Ash Brown', 'Clear: Golden Brown, Red, or Natural brown','Deep: Medium to Deep brown, Black'], key: 'hair' },
    { question: 'What is your eye colour?', options: ['Light: Blue or Green', 'Warm: Blue-green or Hazel', 'Soft: Greyish-Blue or green, or Soft Hazel','Cool: Greyish-blue, Greyish-brown, or Grey','Clear: Bright Blue, Bright Green, Bright Brown','Deep: Dark brown, Black-brown, or Black'], key: 'eyes' },
    { question: 'What is your skintone? Please Select which fits the best if all are not true', options: ['Light: Fair/Porcelin, Burn Easily, Does not tan, Rose or Peach undertone', 'Warm: Gold or Ivory, Fair and Beige (typically freckles), Burns Easily, Does not Tan easily, Peachy or Gold undertone ', 'Soft: Netural Beige or Light Brown, Olive Undertones, May have freckles, Tans Easily ','Cool: Porcelin or Beige, Rosey undertones, Burns Gradually','Clear: Milky White or Fair, Rosey Tones, Burns easily','Deep: Bronze or Rich Brown, neutral or blue undertones, Rarely or Never Burns, Tans Fast'], key: 'skintone' },
    { question: 'What is your best color group?', options: ['Light: Pastels--Baby Pink, Peach, Ash Green, Beige', 'Warm: Beachy--Tan, Coral, Orange, Brown', 'Soft: Salmon, Mauve, Taupe','Cool: Rose Pink, Fuschia, Lavendar, Violet','Clear: Golden Yellow, Bright Red, Hot Pink, Royal Blue','Deep: Mustard, Deep Red, Imperial Purple, Charcoal'], key: 'colors' },
    { question: 'Which lipstick color do you use most often?', options: ['Light: Peach or Light Pink', 'Warm: Coral or Warm Red', 'Soft: Mauve or Cinnamon','Cool: Rose Pink or Fuschia','Clear: Red or Hot Pink','Deep: Cadminum Red or Burgandy'], key: 'lipstick'}
  ];

    /** key
     * hair:
     *  light: 10
     *  warm: 4-6
     *  soft: 7-5
     *  cool: 6-4
     *  clear: 8-4
     *  deep: 4-1
     * 
     * 
     * 
     * 
     * 
     * 
     * 
    */


  const seasons = {
    'Bright Spring': {
      undertone: 'Warm',
      contrast: 'Yes',
      colors: ['Coral', 'Emerald', 'Bright Yellow'],
      theme: 'bg-pink-100 text-pink-900'
    },
    'Soft Summer': {
      undertone: 'Cool',
      contrast: 'No',
      colors: ['Dusty Rose', 'Lavender', 'Steel Blue'],
      theme: 'bg-blue-100 text-blue-900'
    },
    'Deep Winter': {
      undertone: 'Cool',
      contrast: 'Yes',
      colors: ['Crimson', 'Royal Blue', 'Charcoal'],
      theme: 'bg-gray-100 text-gray-900'
    },
    'Warm Autumn': {
      undertone: 'Warm',
      contrast: 'No',
      colors: ['Rust', 'Olive', 'Mustard'],
      theme: 'bg-orange-100 text-orange-900'
    }
  };

  function selectOption(option) {
    const key = quiz[currentQuestion].key;
    selectedAnswers[key] = option;
    if (currentQuestion < quiz.length - 1) {
      currentQuestion++;
    } else {
      matchSeason();
      showResults = true;
    }
  }

  //match if user answers at least two of the same

  function matchSeason() {
    const { eyes, hair, lipstick,skintone } = selectedAnswers;
    if ( eyes === 'Light' &&  hair === 'Light' || eyes === 'Light' && lipstick === 'Light' || eyes === 'Light' && skintone === 'Light' || hair === 'Light' && lipstick === 'Light' || hair === 'Light' && skintone === 'Light' || lipstick === 'Light' && skintone === 'Light') matchedSeason = 'Light Spring';
    else if ( eyes === 'Warm' &&  hair === 'Warm' || eyes === 'Warm' && lipstick === 'Warm' || eyes === 'Warm' && skintone === 'Warm' || hair === 'Warm' && lipstick === 'Warm' || hair === 'Warm' && skintone === 'Warm' || lipstick === 'Warm' && skintone === 'Warm') matchedSeason = 'Warm Autum';
    else if ( eyes === 'Soft' &&  hair === 'Soft' || eyes === 'Soft' && lipstick === 'Soft' || eyes === 'Light' && skintone === 'Soft' || hair === 'Soft' && lipstick === 'Soft' || hair === 'Soft' && skintone === 'Soft' || lipstick === 'Soft' && skintone === 'Soft') matchedSeason = 'Soft Summer';
    else if ( eyes === 'Cool' &&  hair === 'Cool' || eyes === 'Cool' && lipstick === 'Cool' || eyes === 'Cool' && skintone === 'Cool' || hair === 'Cool' && lipstick === 'Cool' || hair === 'Cool' && skintone === 'Cool' || lipstick === 'Cool' && skintone === 'Cool') matchedSeason = 'Cool Summer ';
    else if ( eyes === 'Clear' &&  hair === 'Clear' || eyes === 'Clear' && lipstick === 'Clear' || eyes === 'Clear' && skintone === 'Clear' || hair === 'Clear' && lipstick === 'Clear' || hair === 'Clear' && skintone === 'Clear' || lipstick === 'Clear' && skintone === 'Clear') matchedSeason = 'Bright Winter';
    else if ( eyes === 'Deep' &&  hair === 'Deep' || eyes === 'Deep' && lipstick === 'Deep' || eyes === 'Deep' && skintone === 'Deep' || hair === 'Deep' && lipstick === 'Deep' || hair === 'Deep' && skintone === 'Deep' || lipstick === 'Deep' && skintone === 'Deep') matchedSeason = 'Deep Winter';
  }
</script>

<!-- Leopard Print Background -->
<div
  class="fixed inset-0 bg-cover bg-center flex items-center justify-center z-50"
  style="background-image: url('/leopard.jpg');"
>
  <!-- Translucent Quiz Box -->
  <div class="bg-white/90 backdrop-blur-md rounded-xl shadow-2xl p-6 w-full max-w-md relative animate-fade-in">
    <!-- Smaller Close Button -->
    <button
      on:click={() => dispatch('close')}
      class="absolute top-2 right-2 text-gray-500 hover:text-gray-700 text-sm font-bold"
    >
      ×
    </button>

    {#if !showResults}
      <h2 class="text-xl font-bold mb-4 text-indigo-700">Question {currentQuestion + 1} of {quiz.length}</h2>
      <p class="mb-6 text-gray-800 font-medium">{quiz[currentQuestion].question}</p>
      <div class="space-y-3">
        {#each quiz[currentQuestion].options as option}
          <button
            on:click={() => selectOption(option)}
            class="w-full px-4 py-2 rounded-lg bg-indigo-100 hover:bg-indigo-200 text-indigo-900 font-semibold transition duration-200"
          >
            {option}
          </button>
        {/each}
      </div>
    {:else}
      <div class={`rounded-lg p-4 ${seasons[matchedSeason]?.theme ?? 'bg-gray-100 text-gray-900'}`}>
        <h2 class="text-2xl font-bold mb-2">Your Season: {matchedSeason}</h2>
        <p class="mb-4">Recommended colors for you:</p>
        <ul class="list-disc pl-5 space-y-1">
          {#each seasons[matchedSeason]?.colors ?? [] as color}
            <li class="font-medium">{color}</li>
          {/each}
        </ul>
      </div>
      <button
        on:click={() => dispatch('close')}
        class="mt-6 px-4 py-2 bg-indigo-600 text-white rounded hover:bg-indigo-700 transition"
      >
        Close Quiz
      </button>
    {/if}
  </div>
</div>

<style>
  @keyframes fade-in {
    from { opacity: 0; transform: scale(0.95); }
    to { opacity: 1; transform: scale(1); }
  }
  .animate-fade-in {
    animation: fade-in 0.3s ease-out;
  }
</style>
