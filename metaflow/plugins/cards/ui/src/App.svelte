<script lang="ts">
  // we are importing prism locally because its custom compiled.
  import "./prism";
  import "./global.css";
  import "./prism.css";
  import "./app.css"
  import { cardData, modal } from "./store";
  import * as utils from "./utils";
  import Aside from "./components/aside.svelte";
  import ComponentRenderer from "./components/card-component-renderer.svelte";
  import Main from "./components/main.svelte";
  import Modal from "./components/modal.svelte";
  import Nav from "./components/aside-nav.svelte";

  // Set the `embed` class to hide the `aside` if specified in the URL
  const urlParams = new URLSearchParams(window?.location.search);
  let embed = Boolean(urlParams.get('embed'))
</script>

<div class="container mf-card" class:embed>
  <Aside>
    <Nav pageHierarchy={utils.getPageHierarchy($cardData?.components)} />
  </Aside>

  <Main>
    {#each $cardData?.components || [] as componentData}
      <ComponentRenderer {componentData} />
    {/each}
  </Main>
</div>

{#if $modal}
  <Modal componentData={$modal} />
{/if}

<style>
  .container {
    width: 100%;
    display: flex;
    flex-direction: column;
    position: relative;
  }
</style>
