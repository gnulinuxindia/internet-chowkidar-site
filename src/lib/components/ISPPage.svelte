<script lang="ts">
  type Site = {
    id: number;
    domain: string;
	site_id: number;
    block_reports: number;
    unblock_reports: number;
    last_reported_at: string;
    created_at: string;
    updated_at: string;
  };

  type ISP = {
    id: number;
    latitude: number;
    longitude: number;
    name: string;
    created_at: string;
    updated_at: string;
    blocks: Site[];
  };

  export let isp: ISP;

</script>

<div class="container mx-auto py-10">
  <div class="flex flex-col items-center">


    <h1 class="text-3xl font-bold">{isp.name}</h1>
    <div class="text-sm text-gray-900">{"Last updated at: "+ isp.updated_at}</div>
  </div>
  <div class="mt-10">
    <h2 class="text-xl font-bold">Blocked sites</h2>
    <div class="mt-4">
      <ul>
        {#each isp.blocks as site, index (site.site_id)}
        <li>
          <div class="flex items-center">
            <div class="w-10 h-10 bg-gray-200 rounded-full flex items-center justify-center">
              <span class="text-gray-500">{ index + 1 }</span>
            </div>
            <div class="ml-4">
              <div class="text-lg font-bold"><a href="/sites/{site.site_id}">{ site.domain }</a></div>
              <span class="font-bold text-lg text-red-800">Blocks: { site.block_reports }</span> /
              <span class="font-bold text-lg text-green-600">Unblocks: { site.unblock_reports }</span>
            </div>
          </div>
        {/each}

      </ul>
    </div>
  </div>

</div>
