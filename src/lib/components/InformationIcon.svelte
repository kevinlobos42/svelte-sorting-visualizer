<script>
  import { browser } from "$app/environment";
  import {
    BubbleSortInfo,
    QuickSortInfo,
    MergeSortInfo,
  } from "$lib/components/index";

  export let alg;

  let open = false;

  let scrollTop = Number(null);
  let scrollLeft = Number(null);

  function disableScroll() {
    if (browser) {
      scrollTop =
        window.pageYOffset || window.document.documentElement.scrollTop;
      (scrollLeft =
        window.pageXOffset || window.document.documentElement.scrollLeft),
        (window.onscroll = function () {
          window.scrollTo(scrollLeft, scrollTop);
        });
    }
  }
  function enableScroll() {
    if (browser) {
      window.onscroll = function () {};
    }
  }

  $: if (open) {
    // prevent scroll
    disableScroll();
  } else {
    enableScroll();
  }

</script>

<button class="group relative cursor-pointer" on:click={() => (open = true)}>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="1em"
    height="1em"
    viewBox="0 0 24 24"
    {...$$props}
  >
    <path
      fill="currentColor"
      d="M11 17h2v-6h-2zm1-8q.425 0 .713-.288T13 8t-.288-.712T12 7t-.712.288T11 8t.288.713T12 9m0 13q-2.075 0-3.9-.788t-3.175-2.137T2.788 15.9T2 12t.788-3.9t2.137-3.175T8.1 2.788T12 2t3.9.788t3.175 2.137T21.213 8.1T22 12t-.788 3.9t-2.137 3.175t-3.175 2.138T12 22"
    />
  </svg>
  <p
    class="invisible group-hover:visible font-normal border-2 border-white rounded-sm p-1 absolute left-[120%] top-[-50%] text-nowrap"
  >
    Click for more Information
  </p>
</button>

{#if open}
  {#if open && alg === "Bubble"}
    <BubbleSortInfo bind:open />
  {:else if alg == "Quick"}
    <QuickSortInfo bind:open />
  {:else}
    <MergeSortInfo bind:open />
  {/if}
{/if}
