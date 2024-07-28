<script lang="ts">
  export let isps: Array<{
    id: number;
    latitude: number;
    longitude: number;
    name: string;
    block_reports: number;
    unblock_reports: number;
    last_reported_at: string;
  }>;

</script>

<div class="container mx-auto py-10">
  <table class="min-w-full bg-white shadow-md rounded-lg overflow-hidden">
    <thead class="bg-gray-100">
    <tr>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
        ISP
      </th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
        Total Blocks
      </th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
        Total Unblocks
      </th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600 cursor-pointer">
        Last Reported
      </th>
      <th class="px-4 py-2 text-left text-sm font-semibold text-gray-600">Actions</th>
    </tr>
    </thead>
    <tbody>
    {#each isps as isp(isp.id)}
      <tr class="border-b border-gray-200 hover:bg-gray-50">
        <td class="px-4 py-2">{isp.name}</td>
        <td class="px-4 py-2 text-lg font-bold text-red-800">{isp.block_reports}</td>
        <td class="px-4 py-2 text-lg font-bold text-green-600">{isp.unblock_reports}</td>
        <td class="px-4 py-2">{new Date(isp.last_reported_at).toLocaleString()}</td>
        <td class="px-4 py-2"><a href={"/isps/"+isp.id}><button class="btn-primary btn">View</button></a></td>
      </tr>
    {/each}
    </tbody>
  </table>
</div>