<script>
  import { Button, HoverInfo, InformationIcon } from "$lib/components/index.js";
  /**
   *
   * @param {Number} size
   * @param {Number} ceil
   */
  function makeArr(size, ceil) {
    let arr = [];
    for (let i = 0; i < size; i++) {
      let val = Math.ceil(Math.random() * ceil);
      arr.push(val);
    }
    return arr;
  }
  let size = 100;
  let ceil = 200;
  let maxNodes = 100;
  export let bubbleSortArr = makeArr(size, ceil);
  let disable = false;

  let swappingIndices = { i: -1 };

  /**
   *
   * @param {Array<Number>}arr
   */
  async function bubbleSort(arr) {
    for (let i = arr.length; i >= 0; i--) {
      for (let j = 1; j <= i; j++) {
        if (arr[j - 1] > arr[j]) {
          swappingIndices = { i: j };

          let temp = arr[j - 1];
          arr[j - 1] = arr[j];
          arr[j] = temp;

          bubbleSortArr = [...arr];

          await new Promise((r) => setTimeout(r, 100));

          swappingIndices = { i: -1 };
        }
      }
    }
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeCeil(e) {
    ceil = Number(e.currentTarget.value);
    bubbleSortArr = makeArr(size, ceil);
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeSize(e) {
    size = Number(e.currentTarget.value);
    bubbleSortArr = makeArr(size, ceil);
  }
  $: outerWidth = 0;

  $: if (outerWidth < 600) {
    maxNodes = 35;
    if (size > maxNodes) {
      size = maxNodes;
      bubbleSortArr = makeArr(size, ceil);
    }
  } else if (outerWidth < 1200) {
    maxNodes = 50;
    if (size > maxNodes) {
      size = maxNodes;
      bubbleSortArr = makeArr(size, ceil);
    }
  } else if (outerWidth < 1700) {
    maxNodes = 75;
    if (size > maxNodes) {
      size = maxNodes;
      bubbleSortArr = makeArr(size, ceil);
    }
  } else {
    maxNodes = 100;
  }
</script>

<svelte:window bind:outerWidth />

<section>
  <p class="text-xl font-bold flex items-center gap-3 justify-start">
    Bubble Sort <InformationIcon alg="Bubble" />
  </p>
  <div
    class="flex gap-1 md:gap-2 py-4 h-[500px] w-full justify-center items-center"
  >
    {#each bubbleSortArr as y, idx}
      <p
        id={`BubbleSortNode${idx}`}
        class={`group relative min-w-1 lg:min-w-2 rounded hover:bg-sky-400 cursor-pointer ${idx === swappingIndices.i ? "bg-yellow-300" : "bg-white"}`}
        style="height:{(480 * y) / 200}px"
      >
        <HoverInfo val={y} />
      </p>
    {/each}
  </div>
  <div class="flex flex-col lg:flex-row gap-2 lg:items-center justify-center">
    <Button
      {disable}
      variant="secondary"
      click={() => {
        bubbleSortArr = makeArr(size, ceil);
      }}>Randomize</Button
    >
    <Button
      {disable}
      variant="primary"
      click={async () => {
        disable = true;
        await bubbleSort(bubbleSortArr);
        disable = false;
      }}>Sort</Button
    >
    <input
      disabled={disable}
      type="range"
      name="size"
      min="1"
      max={maxNodes}
      value={size}
      on:change={(e) => changeSize(e)}
    />
    <label for="size">{size} Nodes</label>
    <input
      disabled={disable}
      type="range"
      name="ceil"
      min="1"
      max="200"
      value={ceil}
      on:change={(e) => changeCeil(e)}
    />
    <label for="ceil">Max Height: {ceil}</label>
  </div>
</section>
