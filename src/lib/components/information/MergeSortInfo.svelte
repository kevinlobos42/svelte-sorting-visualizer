<script>
    export let open = false;
</script>

<div
  class="{open
    ? 'visible'
    : 'invisible'} w-full h-[100vh] bg-black bg-opacity-50 fixed top-0 z-50 grid place-items-center"
>
  <div
    class="relative py-6 px-12 border-white bg-black border-2 rounded-md flex flex-col items-center justify-center"
  >
    <div class="h-full w-full">
      <button
        class="absolute right-5 top-2 text-2xl"
        on:click={() => (open = false)}>X</button
      >
      <p class="text-3xl">Merge Sort Explanation</p>
      <p class="font-normal pb-2">
        Merge sort is a sorting algorithm that follows the divide-and-conquer approach.
        It works by recursively dividing the input array into smaller subarrays and
        sorting those subarrays then merging them back together to obtain the sorted array.
      </p>
      <p class="font-normal pb-2">In simple terms, we can say that the process of merge sort is to divide the array
         into two halves, sort each half, and then merge the sorted halves back together.
         This process is repeated until the entire array is sorted.
      </p>
      <img
        src="https://miro.medium.com/v2/resize:fit:1000/0*nh6F_qERbgD3xmV-.gif"
		alt="Merge Sort GIF"
      />
	    <hr class="my-5" />

      <p class="font-normal"><b>Time Complexity</b></p>
      <ul class="font-normal">
        <li><b>Best Case</b>: O(n log n)</li>
        <li><b>Average Case</b>: O(n log n)</li>
        <li><b>Worst Case</b>: O(n log n)</li>
      </ul>
	    <hr class="my-5" />

      <p class="text-2xl">Advantages of Merge Sort:</p>
      <ul class="font-normal list-disc">
        <li><b>Stability</b> : Merge sort is a stable sorting algorithm, which means it maintains the relative order
           of equal elements in the input array.</li>
        <li><b>Guaranteed worst-case performance</b>: Merge sort has a worst-case time complexity of O(N logN) , which
           means it performs well even on large datasets.</li>
        <li>
          <b>Simple to implement</b>: The divide-and-conquer approach is straightforward.
        </li>
        <li>
          <b>Naturally Parallel</b> : We independently merge subarrays that makes it suitable for parallel processing.
        </li>
      </ul>
	    <hr class="my-5" />


      <p class="text-2xl">Disadvantages of Merge Sort:</p>
      <ul class="font-normal list-disc">
        <li><b>Space complexity</b>: Merge sort requires additional memory to store the merged sub-arrays during the sorting process.</li>
        <li><b>Not in-place</b>: Merge sort is not an in-place sorting algorithm, which means it requires additional memory to store
           the sorted data. This can be a disadvantage in applications where memory usage is a concern.
        </li>
        <li><b>Slower than QuickSort in general</b>. QuickSort is more cache friendly because it works in-place.</li>
      </ul>
    </div>
  </div>
</div>