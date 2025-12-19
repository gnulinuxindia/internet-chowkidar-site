<script lang="ts">
  import {
    WebsiteName,
    WebsiteBaseUrl,
    WebsiteDescription,
    ApiUrl,
  } from "../../../config";
  import { onMount } from "svelte"
  import ISPDataTable from "$lib/components/ISPDataTable.svelte"

  const ldJson = {
    "@context": "https://schema.org",
    "@type": "WebSite",
    name: WebsiteName,
    url: WebsiteBaseUrl,
  };
  const jsonldScript = `<script type="application/ld+json">${
    JSON.stringify(ldJson) + "<"
  }/script>`;

  let isps = [];
  let isLoading = true;
  let error = null;

  async function fetchSites() {
    try {
      const response = await fetch(ApiUrl+'/isps'); // Replace with your actual API endpoint
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      isps = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      isLoading = false;
    }
  }

  onMount(fetchSites);
</script>

<svelte:head>
  <title>{WebsiteName}</title>
  <meta name="description" content={WebsiteDescription} />
</svelte:head>

<div class="flex flex-col items-center py-8 justify-center ">
  <div class="text-center mb-8">
    <h1 class="text-2xl font-bold">Current Block Data</h1>
    <span class="text-sm">Below is all the data that we have on internet blocks.</span>
  </div>


  {#if isLoading}
    <p>Loading...</p>
  {:else if error}
    <p>Error: {error}</p>
  {:else}
    <ISPDataTable {isps}/>
  {/if}
</div>
