<script lang="ts">
  import { CircleLayer, GeoJSON, HeatmapLayer, MapLibre } from "svelte-maplibre"
  import Counter from "$lib/components/Counter.svelte"

  type ISP = {
    id: number;
    latitude: number;
    longitude: number;
    name: string;
    block_reports: number;
    unblock_reports: number;
    created_at: string;
    updated_at: string;
  };

  type Site = {
    id: number;
    domain: string;
    categories: string[];
    block_reports: number;
    unblock_reports: number;
    last_reported_at: string;
    blocked_by_isps: ISP[];
    created_at: string;
    updated_at: string;
  };

  export let site: Site;

  const geojsonData = {
    type: 'FeatureCollection',
    features: site.blocked_by_isps.map(isp => ({
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [isp.longitude, isp.latitude]
      },
      properties: {
        id: isp.id,
        name: isp.name,
        block_reports: isp.block_reports,
        unblock_reports: isp.unblock_reports,
        mag: isp.block_reports // Using block_reports as magnitude for visualization
      }
    }))
  };
</script>

<div class="container mx-auto py-10">
  <div class="flex flex-col items-center">


    <h1 class="text-3xl font-bold">{site.domain }</h1>
    <div class="text-sm text-gray-500">{ site.categories.join(', ') }</div>
    <div class="text-sm text-gray-900">{"Last reported at: "+ site.last_reported_at }</div>
  </div>
  <div class="flex md:flex-row items-center justify-evenly mt-4">
    <Counter endValue={site.block_reports} text="Blocks" />
    <Counter endValue={site.unblock_reports} text="Unblocks" />
    <Counter endValue={site.blocked_by_isps.length} text="ISPs" />
  </div>
  <div  class="mt-10 w-20px h-[400px]"> <!-- Fixed size container for the map -->
    <div class="map-wrap">
    <MapLibre
      style="https://basemaps.cartocdn.com/gl/positron-gl-style/style.json"
      standardControls
      center={[78.9629, 20.5937]}
      zoom={4}
    >
      <GeoJSON id="blocks" data={geojsonData}>
        <HeatmapLayer
          maxzoom={9}
          paint={{
              'heatmap-weight': ['interpolate', ['linear'], ['get', 'mag'], 0, 0, 6, 1],
              'heatmap-intensity': ['interpolate', ['linear'], ['zoom'], 0, 1, 9, 3],
              'heatmap-color': [
                'interpolate',
                ['linear'],
                ['heatmap-density'],
                0, 'rgba(33,102,172,0)',
                0.2, 'rgb(103,169,207)',
                0.4, 'rgb(209,229,240)',
                0.6, 'rgb(253,219,199)',
                0.8, 'rgb(239,138,98)',
                1, 'rgb(178,24,43)',
              ],
              'heatmap-radius': ['interpolate', ['linear'], ['zoom'], 0, 2, 9, 20],
              'heatmap-opacity': ['interpolate', ['linear'], ['zoom'], 7, 1, 9, 0],
            }}
        />
        <CircleLayer
          id="blocks-circle"
          source="blocks"
          minzoom={7}
          paint={{
              'circle-radius': [
                'interpolate',
                ['linear'],
                ['zoom'],
                7, ['interpolate', ['linear'], ['get', 'mag'], 1, 1, 6, 4],
                16, ['interpolate', ['linear'], ['get', 'mag'], 1, 5, 6, 50],
              ],
              'circle-color': [
                'interpolate',
                ['linear'],
                ['get', 'mag'],
                1, 'rgba(33,102,172,0)',
                2, 'rgb(103,169,207)',
                3, 'rgb(209,229,240)',
                4, 'rgb(253,219,199)',
                5, 'rgb(239,138,98)',
                6, 'rgb(178,24,43)',
              ],
              'circle-stroke-color': 'white',
              'circle-stroke-width': 1,
              'circle-opacity': ['interpolate', ['linear'], ['zoom'], 7, 0, 8, 1],
            }}
        />
      </GeoJSON>    </MapLibre>
    </div>
  </div>
  <div class="mt-10">
    <h2 class="text-xl font-bold">Blocked by ISPs</h2>
    <div class="mt-4">
      <ul>
        {#each site.blocked_by_isps as isp, index (isp.id)}
        <li>
          <div class="flex items-center">
            <div class="w-10 h-10 bg-gray-200 rounded-full flex items-center justify-center">
              <span class="text-gray-500">{ index + 1 }</span>
            </div>
            <div class="ml-4">
              <div class="text-lg font-bold">{ isp.name }</div>
              <span class="font-bold text-lg text-red-800">Blocks: { isp.block_reports }</span> /
              <span class="font-bold text-lg text-green-600">Unblocks: { isp.unblock_reports }</span>
<!--              <div class="text-sm text-gray-500">{ isp.latitude }, { isp.longitude }</div>-->
            </div>
          </div>
        {/each}

      </ul>
    </div>
  </div>

</div>

<style>
    .map-wrap {
        position: relative;
        width: 100%;
        height: 400px; /* calculate height of the screen minus the heading */
    }

</style>