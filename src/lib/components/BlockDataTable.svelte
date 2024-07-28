<script lang="ts">
  export let sites: Array<{
    site_url: string;
    site_id: number;
    site_total_blocks: number;
    site_total_unblocks: number;
    last_reported: string;
    category: string;
    tags: string[];
  }>;
</script>

<div class="container mx-auto py-10">
  <table class="min-w-full bg-white shadow-md rounded-lg overflow-hidden">
    <thead class="bg-gray-100">
    <tr>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Site URL</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Site ID</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Total Blocks</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Total Unblocks</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Last Reported</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Category</th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Tags</th>
    </tr>
    </thead>
    <tbody>
    {#each sites as site (site.site_id)}
   <tr class="border-b border-gray-200 hover:bg-gray-50">
        <td class="px-4 py-2 text-sm">{site.site_url}</td>
        <td class="px-4 py-2 text-sm">{site.site_id}</td>
        <td class="px-4 py-2 text-sm">{site.site_total_blocks}</td>
        <td class="px-4 py-2 text-sm">{site.site_total_unblocks}</td>
        <td class="px-4 py-2 text-sm">{new Date(site.last_reported).toLocaleString()}</td>
        <td class="px-4 py-2 text-sm">{site.category}</td>
        <td class="px-4 py-2 text-sm">{site.tags.join(', ')}</td>
        <td class="px-4 py-2 text-sm"><a href={"/sites/"+site.site_id}><button class="btn-primary btn">View</button></a></td>
      </tr>
    {/each}
    </tbody>
  </table>
</div>
