<script lang="ts">
  import { setContext } from "svelte";
  import { writable } from "svelte/store";
  import Image from "./Image.svelte";

  let file: HTMLInputElement;
  const image = writable<FileReader["result"]>();

  const onUpload = (e: Event) => {
    const target = e?.target as HTMLInputElement;
    let reader = new FileReader();
    reader.readAsDataURL(target.files![0]);
    reader.onload = (e) => image.set(e.target!.result);
  };

  setContext("image", image);
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  data-name="blob"
  viewBox="0 0 48 48"
  class="sr-only"
>
  <defs>
    <clipPath
      id="clip"
      clipPathUnits="objectBoundingBox"
      transform="scale(0.020833 0.020833)"
    >
      <path
        d="M0 24c0-7.46 0-11.18 1.22-14.12a15.98 15.98 0 0 1 8.66-8.66C12.82 0 16.55 0 24 0s11.18 0 14.12 1.22a15.98 15.98 0 0 1 8.66 8.66C48 12.82 48 16.55 48 24s0 11.18-1.22 14.12a15.98 15.98 0 0 1-8.66 8.66C35.18 48 31.45 48 24 48s-11.18 0-14.12-1.22a15.98 15.98 0 0 1-8.66-8.66C0 35.18 0 31.45 0 24Z"
      />
    </clipPath>
  </defs>
</svg>

<div class="flex flex-col items-center justify-center gap-24">
  <div class="flex gap-16 ml-2">
    <Image rounded />
    <Image />
  </div>
  <label
    for="file-upload"
    class="inline-flex items-center justify-center dark:text-stone-100 border-2 border-indigo-400 hover:border-indigo-500 bg-indigo-400/25 hover:bg-indigo-500/50 transition-all duration-150 ease-in-out px-4 py-2 rounded-full hover:cursor-pointer text-lg font-semibold"
    on:click={() => {
      file.click();
    }}
  >
    Upload Image
  </label>
  <input
    type="file"
    class="hidden"
    accept=".jpg, .jpeg, .png"
    on:change={(e) => onUpload(e)}
    bind:this={file}
  />
</div>
