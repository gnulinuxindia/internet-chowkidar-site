<script lang="ts">
  import {
    WebsiteName,
    WebsiteBaseUrl,
    WebsiteDescription,
    ApiUrl,
  } from "../../../../config";
  import { onMount } from "svelte"
  import { page } from '$app/stores';
  import ISPPage from "$lib/components/ISPPage.svelte"

  const ldJson = {
    "@context": "https://schema.org",
    "@type": "WebSite",
    name: WebsiteName,
    url: WebsiteBaseUrl,
  };
  const jsonldScript = `<script type="application/ld+json">${
    JSON.stringify(ldJson) + "<"
  }/script>`;

  let isp = {};
  let isLoading = true;
  let error = null;

  async function fetchISPs() {
    try {
      const response = await fetch(ApiUrl+`/isps/${$page.params.slug}`);
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      isp = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      isLoading = false;
    }
  }

  onMount(fetchISPs);
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
    <ISPPage {isp} />
  {/if}
</div>
