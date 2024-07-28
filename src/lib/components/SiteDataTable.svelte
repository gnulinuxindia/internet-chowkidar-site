<script lang="ts">

  export let sites: Array<{
    id: number;
    domain: string;
    categories: string[];
    block_reports: number;
    unblock_reports: number;
    last_reported_at: string;
  }>;
</script>

<div class="overflow-auto">
<table class="w-3/4 bg-white sm:overflow-scroll overflow-x-scroll overflow-auto shadow-md rounded-lg ">
  <thead class="bg-gray-100">
  <tr>
    <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
      Domain
    </th>
    <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
      Categories
    </th>
    <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
      Block Reports
    </th>
    <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
      Unblock Reports
    </th>
    <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer" >
      Last Reported
    </th>
  </tr>
  </thead>
  <tbody>
  {#each sites as site (site.id)}
    <tr class="border-b border-gray-200 hover:bg-gray-50">
      <td class="px-4 py-2">{site.domain}</td>
      <td class="px-4 py-2">{site.categories.join(', ')}</td>
      <td class="px-4 py-2 text-red-600">{site.block_reports}</td>
      <td class="px-4 py-2 text-green-600">{site.unblock_reports}</td>
      <td class="px-4 py-2">{new Date(site.last_reported_at).toLocaleString()}</td>
      <td class="px-4 py-2"><a href={"/sites/" + site.id}><button class="btn btn-primary">View</button></a></td>
    </tr>
  {/each}
  </tbody>
</table>
</div>