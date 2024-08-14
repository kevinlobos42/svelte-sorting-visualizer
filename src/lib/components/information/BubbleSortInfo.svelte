<script>
    export let open = false;
</script>

<div
  class="{open
    ? 'visible'
    : 'invisible'} w-full h-[100vh] bg-black bg-opacity-50 fixed z-50 top-0 grid place-items-center"
>
  <div
    class="relative py-6 px-12 border-white bg-black border-2 rounded-md flex flex-col items-center justify-center"
  >
    <div class="h-full w-full">
      <button
        class="absolute right-5 top-2 text-2xl"
        on:click={() => (open = false)}>X</button
      >
      <p class="text-3xl">Bubble Sort Explanation</p>
      <p class="font-normal">
        Bubble sort algorithm works by repeatedly swapping adjacent elements if
        thay are not in the correct order. Works for small data sets but it is
        not suitable for large sets as its time complexity is quite high
      </p>
      <img
        src="https://miro.medium.com/v2/resize:fit:1000/0*nh6F_qERbgD3xmV-.gif"
		alt="Bubble Sort GIF"
      />
	    <hr class="my-5" />

      <p class="font-normal"><b>Time Complexity</b>: O(N^2)</p>
	    <hr class="my-5" />

      <p class="text-2xl">Advantages of Bubble Sort:</p>
      <ul class="font-normal list-disc">
        <li>Bubble sort is easy to understand and implement.</li>
        <li>It does not require any additional memory space.</li>
        <li>
          It is a stable sorting algorithm, meaning that elements with the same
          key value maintain their relative order in the sorted output.
        </li>
      </ul>
	    <hr class="my-5" />


      <p class="text-2xl">Disadvantages of Bubble Sort:</p>
      <ul class="font-normal list-disc">
        <li>
          Bubble sort has a time complexity of O(N^2) which makes it very slow
          for large data sets.
        </li>
        <li>
          Bubble sort is a comparison-based sorting algorithm, which means that
          it requires a comparison operator to determine the relative order of
          elements in the input data set. It can limit the efficiency of the
          algorithm in certain cases.
        </li>
      </ul>
    </div>
  </div>
</div>