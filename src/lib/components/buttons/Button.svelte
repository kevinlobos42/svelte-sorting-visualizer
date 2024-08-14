<script>
  export let variant = 'primary';
  export let disable;
  export let click = ()=>{}
</script>

<button
  disabled={disable}
  class={`${
    variant === "primary"
      ? "bg-white text-black hover:bg-black hover:text-white border-white border-2 rounded-lg font-normal transition-all duration-200"
      : "border-black border-2 rounded-lg text-white font-normal hover:bg-white hover:text-black transition-all duration-200"
  } font-bold py-2 px-4 rounded`}
  on:click={click()}
>
    <slot></slot>
</button>
