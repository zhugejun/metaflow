<!-- This component will wrap a page.  Later we can decide if we want to render only a single page -->
<script lang="ts">
  import type * as types from "../types";
  export let componentData: types.PageComponent;
  const { title } = componentData;
</script>

<div id={`page-${title || "No Title"}`} class="page">
  <slot />
</div>

<style>
  .page:last-of-type {
    margin-bottom: var(--component-spacer);
  }

  :global(.page:last-of-type section:last-of-type hr) {
    display: none;
  }
</style>
