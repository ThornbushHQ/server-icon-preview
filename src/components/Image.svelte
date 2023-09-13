<script lang="ts">
  import { getContext } from "svelte";
  import type { Writable } from "svelte/store";

  export let rounded = false;

  $: image = "" as FileReader["result"];
  const imageStore = getContext("image") as Writable<FileReader["result"]>;
  imageStore.subscribe((val) => (image = val));
</script>

<figure class="space-y-4">
  <div
    class={`w-32 h-32 md:w-48 md:h-48 lg:w-64 lg:h-64 bg-indigo-400 ${
      rounded ? "rounded-full" : "[clip-path:_url(#clip)]"
    }`}
  >
    {#if image}
      <img
        src={image.toString()}
        alt="user uploaded"
        class={`w-full h-full object-cover ${rounded ? "rounded-full" : ""}`}
      />
    {/if}
  </div>
  <figcaption class="text-xl font-semibold dark:text-white">
    {#if rounded}
      Rounded
    {:else}
      Squircle
    {/if}
  </figcaption>
</figure>
