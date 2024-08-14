<script>
  import { BubbleSort } from "$lib/components/index.js";
  import { QuickSort } from "$lib/components/index.js";
  import { MergeSort } from "$lib/components/index.js";
</script>

<div class="bg-black text-white py-5 px-4">
  <h1 class="text-3xl font-bold text-center">Sorting Algorithms Simulator!</h1>
  <BubbleSort />
  <hr class="my-5" />
  <QuickSort />
  <hr class="my-5" />
  <MergeSort />
  <hr class="my-5" />
  
</div>
<!-- making sure to set lang="postcss" for any <style> blocks that need to be processed by Tailwind. -->
