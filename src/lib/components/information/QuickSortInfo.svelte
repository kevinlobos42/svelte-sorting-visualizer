<script>
  export let open = false;
</script>

<div
  class="{open
    ? 'visible'
    : 'invisible'} w-[100vw] h-[100vh] bg-black bg-opacity-50 fixed z-50 top-0 left-0 grid place-items-center"
>
  <div
    class="overflow-y-auto max-h-[80vh] h-full max-w-[90vw] relative py-6 border-white bg-black border-2 rounded-md flex flex-col items-center justify-center"
  >
    <div class="h-full w-full px-8">
      <button
        class="absolute right-5 top-2 text-2xl"
        on:click={() => (open = false)}>X</button
      >
      <p class="text-3xl">Quick Sort Explanation</p>
      <p class="font-normal pb-2">
        QuickSort is a sorting algorithm based on the Divide and Conquer
        algorithm that picks an element as a pivot and partitions the given
        array around the picked pivot by placing the pivot in its correct
        position in the sorted array. <b
          >The Pivot selection is the most important part of this algorithm.</b
        >
      </p>
      <img
        src="https://sp-ao.shortpixel.ai/client/to_webp,q_lossless,ret_img,w_765,h_255/https://blog.shahadmahmud.com/wp-content/uploads/2020/04/qs1-1.gif"
        alt="Quick Sort GIF"
      />
      <hr class="my-5" />

      <p class="font-normal"><b>Time Complexity</b></p>
      <ul class="font-normal">
        <li><b>Best Case</b>: Ω (N log (N))</li>
        The best-case scenario for quicksort occur when the pivot chosen at the each
        step divides the array into roughly equal halves. In this case, the algorithm
        will make balanced partitions, leading to efficient Sorting.
        <li><b>Average Case</b>: θ ( N log (N))</li>
        Quicksort’s average-case performance is usually very good in practice, making
        it one of the fastest sorting Algorithm.
        <li><b>Worst Case</b>: O(N ^ 2)</li>
        The worst-case Scenario for Quicksort occur when the pivot at each step consistently
        results in highly unbalanced partitions. When the array is already sorted
        and the pivot is always chosen as the smallest or largest element. To mitigate
        the worst-case Scenario, various techniques are used such as choosing a good
        pivot (e.g., median of three) and using Randomized algorithm (Randomized
        Quicksort ) to shuffle the element before sorting.
      </ul>
      <hr class="my-5" />

      <p class="text-2xl">Advantages of Quick Sort:</p>
      <ul class="font-normal list-disc">
        <li>
          It is a divide-and-conquer algorithm that makes it easier to solve
          problems.
        </li>
        <li>It is efficient on large data sets.</li>
        <li>
          It has a low overhead, as it only requires a small amount of memory to
          function.
        </li>
        <li>
          It is Cache Friendly as we work on the same array to sort and do not
          copy data to any auxiliary array.
        </li>
        <li>
          Fastest general purpose algorithm for large data when stability is not
          required.
        </li>
        <li>
          It is tail recursive and hence all the tail call optimization can be
          done.
        </li>
      </ul>
      <hr class="my-5" />

      <p class="text-2xl">Disadvantages of Quick Sort:</p>
      <ul class="font-normal list-disc">
        <li>
          It has a worst-case time complexity of O(N 2 ), which occurs when the
          pivot is chosen poorly.
        </li>
        <li>It is not a good choice for small data sets.</li>
        <li>
          It is not a stable sort, meaning that if two elements have the same
          key, their relative order will not be preserved in the sorted output
          in case of quick sort, because here we are swapping elements according
          to the pivot’s position (without considering their original
          positions).
        </li>
      </ul>
    </div>
  </div>
</div>
