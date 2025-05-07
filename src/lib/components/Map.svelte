<script lang="ts">
  import { onMount } from 'svelte';
  import * as L from 'leaflet';
  import 'leaflet/dist/leaflet.css';

  export let lat: number | string = 0;
  export let lng: number | string = 0;
  export let zoom: number = 14;

  let map: L.Map;
  let mapContainer: HTMLDivElement;

  const parseCoordinate = (coord: number | string): number => {
    return typeof coord === 'string' ? parseFloat(coord) : coord;
  }

  onMount(() => {
    delete (L.Icon.Default.prototype as any)._getIconUrl;
      L.Icon.Default.mergeOptions({
        iconRetinaUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-icon-2x.png',
        iconUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-icon.png',
        shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-shadow.png',
      });

    // Initialize map only in browser
    if (typeof window !== 'undefined') {
      const numericLat = parseCoordinate(lat);
      const numericLng = parseCoordinate(lng);
      map = L.map(mapContainer).setView([numericLat, numericLng], zoom);

      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map);

      // Add marker
      L.marker([numericLat, numericLng])
        .addTo(map)
        .bindPopup('Your location')
        .openPopup();
    }

    return () => {
      if (map) map.remove();
    };
  });

  // Update map when coordinates change
  $: if (map && lat && lng) {
    const numericLat = parseCoordinate(lat);
    const numericLng = parseCoordinate(lng);
    map.setView([numericLat, numericLng], zoom);
    L.marker([numericLat, numericLng]).addTo(map);
  }
</script>

<div class="map-container" bind:this={mapContainer}></div>

<style>
  .map-container {
    height: 400px;
    width: 100%;
    border-radius: 8px;
    margin: 1rem 0;
  }
</style>
