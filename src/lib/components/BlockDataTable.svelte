<script lang="ts">
  export let sites: Array<{
    domain: string;
    id: number;
    block_reports: number;
    unblock_reports: number;
    last_reported_at: string;
    categories: string[];
  }>;
</script>

<div class="container mx-auto py-10">
  <table class="min-w-full bg-white shadow-md rounded-lg overflow-hidden">
    <thead class="bg-gray-100">
    <tr>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Site URL</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Total Blocks</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Total Unblocks</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Last Reported</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Tags</th>
    </tr>
    </thead>
    <tbody>
    {#each sites as site (site.site_id)}
   <tr class="border-b border-gray-200 hover:bg-gray-50">
        <td class="px-4 py-2 text-sm">{site.domain}</td>
        <td class="px-4 py-2 text-sm">{site.block_reports}</td>
        <td class="px-4 py-2 text-sm">{site.unblock_reports}</td>
        <td class="px-4 py-2 text-sm">{new Date(site.last_reported_at).toLocaleString()}</td>
        <td class="px-4 py-2 text-sm">{site.categories.join(" , ")}</td>
        <td class="px-4 py-2 text-sm"><a href={"#"}><button class="btn-primary btn">View</button></a></td>
      </tr>
    {/each}
    </tbody>
  </table>
</div>
