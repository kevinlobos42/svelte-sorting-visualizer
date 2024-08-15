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
  let speed = 50;
  let maxNodes = 100;
  let maxSpeed = 1000;
  export let mergeSortArr = makeArr(size, ceil);
  let disable = false;

  let section = { left: -1, right: -1 };
  /**
   *
   * @param {Array<Number>}arr
   * @param {Number}left
   * @param {Number}mid
   * @param {Number}right
   *
   */
  async function merge(arr, left, mid, right) {
    section.left = left;
    section.right = right;
    const n1 = mid - left + 1;
    const n2 = right - mid;

    // 2 arrays L and R
    const L = arr.slice(left, mid + 1);
    const R = arr.slice(mid + 1, right + 1);

    let i = 0,
      j = 0;
    let k = left;

    // Merge 2 temp Arrays
    while (i < n1 && j < n2) {
      if (L[i] <= R[j]) {
        arr[k] = L[i];
        i++;
      } else {
        arr[k] = R[j];
        j++;
      }
      k++;
      mergeSortArr = [...arr]; // Update the array to trigger reactivity
      await new Promise((r) => setTimeout(r, speed)); // Adjust delay as needed
    }

    // Copy remaining elements of L[]
    while (i < n1) {
      arr[k] = L[i];
      i++;
      k++;
      mergeSortArr = [...arr]; // Update the array to trigger reactivity
      await new Promise((r) => setTimeout(r, speed)); // Adjust delay as needed
    }

    // Copy remaining elemnts of R[]
    while (j < n2) {
      arr[k] = R[j];
      j++;
      k++;
      mergeSortArr = [...arr]; // Update the array to trigger reactivity
      await new Promise((r) => setTimeout(r, speed)); // Adjust delay as needed
    }

    section.left = -1;
    section.right = -1;
  }

  /**
   *
   * @param {Array<Number>}arr
   * @param {Number}left
   * @param {Number}right
   *
   */
  async function mergeSort(arr, left, right) {
    if (left >= right) return;
    const mid = Math.floor(left + (right - left) / 2);
    await mergeSort(arr, left, mid);
    await mergeSort(arr, mid + 1, right);
    await merge(arr, left, mid, right);
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeCeil(e) {
    ceil = Number(e.currentTarget.value);
    mergeSortArr = makeArr(size, ceil);
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeSize(e) {
    size = Number(e.currentTarget.value);
    mergeSortArr = makeArr(size, ceil);
  }
  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeSpeed(e) {
    speed = Number(e.currentTarget.value);
  }

  $: outerWidth = 0;

  $: if (outerWidth < 600) {
    maxNodes = 35;
    if (size > maxNodes) {
      size = maxNodes;
      mergeSortArr = makeArr(size, ceil);
    }
  } else if (outerWidth < 1200) {
    maxNodes = 50;
    if (size > maxNodes) {
      size = maxNodes;
      mergeSortArr = makeArr(size, ceil);
    }
  } else if (outerWidth < 1700) {
    maxNodes = 75;
    if (size > maxNodes) {
      size = maxNodes;
      mergeSortArr = makeArr(size, ceil);
    }
  } else {
    maxNodes = 100;
  }
</script>

<svelte:window bind:outerWidth />

<section>
  <p class="text-xl font-bold flex items-center gap-3 justify-start">
    Merge Sort <InformationIcon alg="Merge" />
  </p>
  <div
    class="flex gap-1 md:gap-2 py-4 h-[500px] w-full justify-center items-center"
  >
    {#each mergeSortArr as y, idx}
      <p
        class={`group relative min-w-1 lg:min-w-2 rounded transition-all duration-200 hover:bg-sky-400 cursor-pointer ${section.left !== -1 && section.right !== -1 && section.left <= idx && idx <= section.right ? "bg-yellow-400" : "bg-white"}`}
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
        mergeSortArr = makeArr(size, ceil);
      }}>Randomize</Button
    >
    <Button
      {disable}
      variant="primary"
      click={async () => {
        disable = true;
        await mergeSort([...mergeSortArr], 0, mergeSortArr.length - 1);
        disable = false;
      }}>Sort</Button
    >
    <input
      disabled={disable}
      type="range"
      name="size"
      min="2"
      max={maxNodes}
      value={size}
      on:change={(e) => changeSize(e)}
    />
    <label for="size">{size} Nodes</label>
    <input
      disabled={disable}
      type="range"
      name="ceil"
      min="2"
      max="200"
      value={ceil}
      on:change={(e) => changeCeil(e)}
    />
    <label for="ceil">Max Height: {ceil}</label>
    <input
      disabled={disable}
      type="range"
      name="Speed"
      min="5"
      max={maxSpeed}
      value={speed}
      on:change={(e) => changeSpeed(e)}
    />
    <label for="Speed">Sorting Speed: {speed}ms</label>
  </div>
</section>
