<script lang="ts">
  import Map from "$lib/components/Map.svelte";
  
  const browserInfo = {
    userAgent: navigator.userAgent,
    platform: navigator.platform,
    vendor: navigator.vendor,
    appName: navigator.appName,
    appVersion: navigator.appVersion,
    language: navigator.language,
    languages: navigator.languages,
    cookieEnabled: navigator.cookieEnabled,
    doNotTrack: navigator.doNotTrack,
    macTouchPoints: navigator.maxTouchPoints,
  }

  const screenInfo = {
    width: screen.width,
    height: screen.height,
    colorDepth: screen.colorDepth,
    pixelDepth: screen.pixelDepth,
    orientation: screen.orientation.type,
    availableWidth: screen.availWidth,
    availableHeight: screen.availHeight
  };

  interface Geolocation {
    latitude: number;
    longitude: number;
    accuracy: number;
    altitude: number | null;
    speed: number | null;
    heading: number | null; 
  }

  let locationInfo: Geolocation = {
    latitude: 0,
    longitude: 0,
    accuracy: 0,
    altitude: null,
    speed: null,
    heading: null
  }

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(position => {
      locationInfo.latitude = position.coords.latitude;
      locationInfo.longitude = position.coords.longitude;
      locationInfo.accuracy= position.coords.accuracy;
      locationInfo.altitude= position.coords.altitude;
      locationInfo.speed = position.coords.speed;
      locationInfo.heading= position.coords.heading;
    }, error => {console.error("Geolocation error", error);})
  }

  const networkInfo = {
    online: navigator.onLine,
    connection: navigator.connection ? {
      effectiveType: navigator.connection.effectiveType,
      downlink: navigator.connection.downLink,
      rtt: navigator.connection.rtt,
      saveData: navigator.connection.saveData
    } : null
  };

  const storageInfo = {
    localStorage: 'localStorage' in window,
    sessionStorage: 'sessionStorage' in window,
    indexedDB: 'indexedDB' in window,
    cookiesEnabled: navigator.cookieEnabled,
    serviceWorker: 'serviceWorker' in navigator,
    cacheStorage: 'caches' in window
  };

  const timeInfo = {
    timezone: Intl.DateTimeFormat().resolvedOptions().timeZone,
    offset: new Date().getTimezoneOffset(),
    date: new Date().toString(),
    locale: Intl.DateTimeFormat().resolvedOptions().locale,
    clockDrift: performance.now() - Date.now()
  };

  interface Motion {
    acceleration: DeviceMotionEventAcceleration | null,
    accelerationIncludingGravity: DeviceMotionEventAcceleration | null,
    rotation: DeviceMotionEventRotationRate | null,
    interval: number
  }

  let motionInfo: Motion;

  window.DeviceMotionEvent ? window.addEventListener('devicemotion', event => {
    motionInfo = {
      acceleration: event.acceleration,
      accelerationIncludingGravity: event.accelerationIncludingGravity,
      rotation: event.rotationRate,
      interval: event.interval
    };
  }) : motionInfo = {
    acceleration: null,
    accelerationIncludingGravity: null,
    rotation: null,
    interval: 0
  };

</script>

<div class="main-container">
  <h1>Datos Visibles</h1>
  <p>
    la sigiente información es solamente una muestra de lo que se puede recopilar desde el navegador,
    ninguna de esta información esta siendo almacenada o enviada a algún otro lado.
  </p>
  <div class="delicate-info">
    <h2>Información del Navegador</h2>
    <ul class="Browser Device Info">
      <li><strong>Modelo de Navegador:</strong> {browserInfo.userAgent}</li>
      <li><strong>Plataforma:</strong> {browserInfo.platform}</li>
      <li><strong>Propietario:</strong> {browserInfo.vendor}</li>
      <li><strong>Nombre de Aplicación:</strong> {browserInfo.appName}</li>
      <li><strong>Versión:</strong> {browserInfo.appVersion}</li>
      <li><strong>Lenguage:</strong> {browserInfo.language}</li>
      <li><strong>Lenguages:</strong> {browserInfo.languages}</li>
      <li><strong>Cookies Habilitadas:</strong> {browserInfo.cookieEnabled}</li>
      <li><strong>No Trackeo:</strong> {browserInfo.doNotTrack}</li>
      <li><strong>Mac touch points:</strong> {browserInfo.macTouchPoints}</li>
    </ul>
    <h2>Información de Pantalla</h2>
    <ul class="Screen Info">
      <li><strong>Ancho:</strong> {screenInfo.width}px</li>
      <li><strong>Alto:</strong> {screenInfo.height}px</li>
      <li><strong>Profundidad de color:</strong> {screenInfo.colorDepth}</li>
      <li><strong>Profundidad de pixel</strong> {screenInfo.pixelDepth}</li>
      <li><strong>Orientación:</strong> {screenInfo.orientation}</li>
      <li><strong>Espacio Vertical Disponible:</strong> {screenInfo.availableWidth}px</li>
      <li><strong>Espacio Horizontal Disponible:</strong> {screenInfo.availableHeight}px</li>
    </ul>  
    <h2>Información de Localización</h2>
    <Map lat={locationInfo.latitude} lng={locationInfo.longitude}}/>
    <ul class="Geolocation">
      <li><strong>Latitud: </strong> {locationInfo.latitude}</li>
      <li><strong>Longitud: </strong> {locationInfo.longitude}</li>
      <li><strong>Exactitud: </strong> {locationInfo.accuracy}</li>
      <li><strong>Altitud: </strong> {locationInfo.altitude}</li>
      <li><strong>Velocidad: </strong> {locationInfo.speed}</li>
      <li><strong>Dirección: </strong> {locationInfo.heading}</li>
    </ul>
    <h2>Información de red</h2>
    <ul class="Network">
      <li><strong>En linea?: </strong> {networkInfo.online}</li>
      <li><strong>Tipo: </strong> {networkInfo.connection?.effectiveType}</li>
      <li><strong>Downlink: </strong> {networkInfo.connection?.downlink}</li>
      <li><strong>Rtt: </strong> {networkInfo.connection?.rtt}</li>
      <li><strong>Información Almacenada: </strong> {networkInfo.connection?.saveData}</li>
    </ul>
    <h2>Información de Almacenamiento</h2>
    <ul class="Storage">
      <li><strong>Almacenamiento Local: </strong> {storageInfo.localStorage}</li>
      <li><strong>Almacenamiento de Sesión: </strong> {storageInfo.sessionStorage}</li>
      <li><strong>Base de Datos indexada: </strong> {storageInfo.indexedDB}</li>
      <li><strong>Cookies: </strong> {storageInfo.cookiesEnabled}</li>
      <li><strong>Trabajador de Servicio: </strong> {storageInfo.serviceWorker}</li>
      <li><strong>Memoria Cache: </strong> {storageInfo.cacheStorage}</li>
    </ul>
    <h2>Información de Tiempo</h2>
    <ul class="Time">
      <li><strong>Zona horaria: </strong> {timeInfo.timezone}</li>
      <li><strong>Variación: </strong> {timeInfo.offset}</li>
      <li><strong>Fecha: </strong> {timeInfo.date}</li>
      <li><strong>Localización: </strong> {timeInfo.locale}</li>
      <li><strong>Variación de Reloj: </strong> {timeInfo.clockDrift}</li>
    </ul>
    <h2>Información de movimiento</h2>
    <ul class="Motion">
      <li><strong>Aceleración: </strong> {motionInfo?.acceleration}</li>
      <li><strong>Aceleración incluyendo gravedad: </strong> {motionInfo?.accelerationIncludingGravity}</li>
      <li><strong>Rotación: </strong> {motionInfo?.rotation}</li>
      <li><strong>Intervalo: </strong> {motionInfo?.interval}</li>
    </ul>
  </div>
</div>

<style>
  .main-container {
    margin-top: 5rem;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
