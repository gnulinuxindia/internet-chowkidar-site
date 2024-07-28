<script lang="ts">
  import {
    WebsiteName,
    WebsiteBaseUrl,
    WebsiteDescription,
  } from "../../../../config";
  import { onMount } from "svelte"
  import { page } from '$app/stores';
  import SitePage from "$lib/components/SitePage.svelte"

  const ldJson = {
    "@context": "https://schema.org",
    "@type": "WebSite",
    name: WebsiteName,
    url: WebsiteBaseUrl,
  };
  const jsonldScript = `<script type="application/ld+json">${
    JSON.stringify(ldJson) + "<"
  }/script>`;

  let site  = {};
  let isLoading = true;
  let error = null;

  async function fetchSites() {
    try {
      const response = await fetch(`https://inetc.kat.directory/sites/${$page.params.slug}`); // Replace with your actual API endpoint
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      site = await response.json();
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



  {#if isLoading}
    <p>Loading...</p>
  {:else if error}
    <p>Error: {error}</p>
  {:else}
    <SitePage {site} />
  {/if}
</div>