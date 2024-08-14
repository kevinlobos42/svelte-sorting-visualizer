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
  export let quickSortArr = makeArr(size, ceil);
  let disable= false

  let pivotIdx = -1;

  /**
   *
   * @param {Number} left
   * @param {Number} right
   * @param {Array<Number>} arr
   */
  function swap(left, right, arr) {
    let temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    quickSortArr = [...arr];
  }

  /**
   *
   * @param {Number} low
   * @param {Number} high
   * @param {Array<Number>} arr
   */
  async function partition(arr, low, high) {
    let pivot = arr[high];
    pivotIdx = high;
    let i = low - 1;
    for (let j = low; j < high; j++) {
      if (arr[j] < pivot) {
        i++;
        [arr[i], arr[j]] = [arr[j], arr[i]];
        quickSortArr = [...arr];

        await new Promise((r) => setTimeout(r, 20));
      }
    }
    [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
    quickSortArr = [...arr];

    await new Promise((r) => setTimeout(r, 100));

    return i + 1;

    pivotIdx = -1
  }

  /**
   *
   * @param {Array<Number>}arr
   *
   */
  async function quickSort(arr, low = 0, high = arr.length - 1) {
    if (low < high) {
      let pivot = await partition(arr, low, high);
      await quickSort(arr, low, pivot - 1);
      await quickSort(arr, pivot + 1, high);
      pivotIdx = -1
    }
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeCeil(e) {
    ceil = Number(e.currentTarget.value);
    quickSortArr = makeArr(size, ceil);
  }

  /**
   *
   * @param {Event & { currentTarget: HTMLInputElement }} e
   */
  function changeSize(e) {
    size = Number(e.currentTarget.value);
    quickSortArr = makeArr(size, ceil);
  }
</script>

<section>
  <p class="text-xl font-bold flex items-center gap-3 justify-start">Quick Sort <InformationIcon alg="Quick"/></p>
  <div class="flex gap-3 py-4 h-[500px] w-full justify-center items-center">
    {#each quickSortArr as y, idx}
      <p
        class={`group relative w-3 rounded transition-all duration-200 hover:bg-sky-400 cursor-pointer ${pivotIdx === idx ? 'bg-yellow-400': 'bg-white'}`}
        style="height:{(480 * y) / 200}px"
      >
        <HoverInfo val={y} />
      </p>
    {/each}
  </div>
  <Button
    disable={disable} 
    variant="secondary"
    click={() => {
      quickSortArr = makeArr(size, ceil);
    }}>Randomize</Button
  >
  <Button
    disable={disable}
    variant="primary"
    click={async () => {disable = true;await quickSort([...quickSortArr]); disable=false;}}>Sort</Button
  >
  <input
    disabled={disable}
    type="range"
    name="size"
    min="1"
    max="100"
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
</section>
