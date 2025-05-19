<script lang="ts">
  import D3Chart from "$lib/components/D3Chart.svelte";
  import Scatter from "$lib/components/Scatter.svelte";
  import Battery from "$lib/components/Battery.svelte";

  interface Skate {
    name: string;
    img: string;
    price: number;
    battery: string;
    top_speed: number;
    range: number;
    weight: number;
    max_load: number;
  }

  let boards:  Skate[] = [
    {
      name: "Wowgo 3E",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-3e-electric-skateboard-longboard-668434.jpg?v=1743667627",
      price: 439,
      battery: "12S2P 216Wh 43.2V 5.0Ah",
      top_speed: 45,
      range: 21,
      weight: 7.5,
      max_load: 150,
    },
    {
      name: "Wowgo 2S Max",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-2s-max-electric-skateboard-longboard-194722.jpg?v=1743667572",
      price: 399,
      battery: "12S2P 216Wh",
      top_speed: 45,
      range: 23,
      weight: 8.2,
      max_load: 150,
    },
    {
      name: "Maxfind Max 5s",
      img: "https://www.maxfind.com/cdn/shop/files/MAXFIND-MAX5-_NEW_-Maxfind-9692.jpg?v=1705550233&width=1000",
      price: 439,
      battery: "Samsung 18650 10S2P, 4.4Ah, 158.4Wh, 36V",
      top_speed: 40,
      range: 25,
      weight: 9.3,
      max_load: 150,
    },
    {
      name: "Meepo Edge",
      img: "https://www.meepoboard.com/cdn/shop/files/meepoedge6.jpg?v=1742806232&width=1080",
      price: 519,
      battery: "345.6Wh 8Ah",
      top_speed: 42,
      range: 32,
      weight: 9.0,
      max_load: 150,
    },
    {
      name: "Tynee Mini 3 SL",
      img: "https://tyneeboard.com/cdn/shop/files/Tynee-Mini-3-SL-Electric-Skateboard-With-105mm-Wheels-2_1600x.jpg?v=1744362407",
      price: 399,
      battery: "6Ah 216WH / 8Ah 288WH",
      top_speed: 45,
      range: 32,
      weight: 8.4,
      max_load: 150,
    },
    {
      name: "Backfire Nalu",
      img: "https://www.backfireboards.com/cdn/shop/files/Cube-S1_1024x1024.jpg?v=1728398122",
      price: 599,
      battery: "136.8Wh 30.4V 4.5Ah",
      top_speed: 25,
      range: 20,
      weight: 5.8,
      max_load: 110,
    },
    {
      name: "Exway Wave Riot",
      img: "https://tremor.fun/cdn/shop/files/ExwayWaveRiotTopandBottom_1080x_a06e35dd-8b5a-4a33-b6af-d1268f00e499.jpg?v=1694130189",
      price: 739,
      battery: "144Wh, 10S2p 42V 24A Smart BMW",
      top_speed: 38,
      range: 20,
      weight: 6.9,
      max_load: 200,
    },
    {
      name: "Meepo Go",
      img: "https://www.meepoboard.com/cdn/shop/files/MEEPOGO6.jpg?v=1739775641&width=1080",
      price: 529,
      battery: "50.4V -12S2P /345Wh/8Ah",
      top_speed: 45,
      range: 32,
      weight: 9.0,
      max_load: 150,
    },
    {
      name: "Exway Flex 2024 SE",
      img: "data:image/jpeg;base64,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",
      price: 649,
      battery: "216Wh 12S2P 51V 40Ah Smart BMS",
      top_speed: 45,
      range: 28,
      weight: 7.9,
      max_load: 150,
    },
    {
      name: "Meepo FLow",
      img: "https://www.meepoboard.com/cdn/shop/files/Flow_8ce9e5db-31c9-4c8c-82cd-60d198b18955.jpg?v=1739511723&width=1080",
      price: 699,
      battery: "50.4V - 12S2P molicel P42A 362Wh / 8.4Ah",
      top_speed: 52,
      range: 38,
      weight: 9.7,
      max_load: 150,
    },
    {
      name: "Propel Pivot GT",
      img: "https://www.ridepropel.com/wp-content/uploads/2023/06/pivot-S-2.png",
      price: 999,
      battery: "864Wh Samsung Cells 12S4P 50S",
      top_speed: 60,
      range: 87,
      weight: 14.5,
      max_load: 150,
    },
    {
      name: "Wowgo AT 2 Plus",
      img: "https://wowgoboard.com/cdn/shop/products/wowgo-at2-plus-electric-skateboard-longboard-443859.jpg?v=1743667876",
      price: 899,
      battery: "604Wh 14Ah 12S4P configuration",
      top_speed: 50,
      range: 45,
      weight: 13.6,
      max_load: 150,
    },
    {
      name: "Propel Endeavor 3S",
      img: "https://www.ridepropel.com/wp-content/uploads/2024/04/END-3S-1.png",
      price: 999,
      battery: "12S4P Lishen LR2170LA 48 cells",
      top_speed: 55,
      range: 38,
      weight: 20,
      max_load: 150,
    },
    {
      name: "Meepo Voyager X Limited",
      img: "https://www.meepoboard.com/cdn/shop/files/voyager_xl_4bb4bfab-7f21-4e4a-bc20-ee41e3698ad1.jpg?v=1739511903&width=2048",
      price: 1099,
      battery: "12S4P Lishen LR2170LA 48 cells",
      top_speed: 60,
      range: 49,
      weight: 11,
      max_load: 150,
    },
    {
      name: "Meepo Vader",
      img: "https://www.meepoboard.com/cdn/shop/files/Vader-Hurricane_Carbon.jpg?v=1739511611&width=1080",
      price: 1599,
      battery: "12S4P Samsung 50S (864Wh / 20Ah)",
      top_speed: 52,
      range: 50,
      weight: 17.6,
      max_load: 250,
    },
    {
      name: "Acedeck Nomad N3",
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQCmKNyaTK7gfZmQ7wZXx2YsY3JfG1pUqLr-g&s",
      price: 1424,
      battery: "14S6P Samsung 50E",
      top_speed: 60,
      range: 90,
      weight: 20.1,
      max_load: 150,
    },
    {
      name: "Acedeck Nyx Z3",
      img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQhCSjE5J6dKH4zsztafJbHNz0XzHvLzzYA5zBhHvCk9sPT6A4nRPPOCpMumPN1s1mgxcY&usqp=CAU",
      price: 1599,
      battery: "14S6P Samsung 50E",
      top_speed: 60,
      range: 95,
      weight: 22.1,
      max_load: 150,
    },
    {
      name: "Propel X4R",
      img: "https://www.ridepropel.com/wp-content/uploads/2024/05/X4R-%E6%B8%B2%E6%9F%931.png",
      price: 2799,
      battery: "Samsung 50S 12S7P 1512Wh 5000Mah",
      top_speed: 60,
      range: 68,
      weight: 45.0,
      max_load: 150,
    },
    {
      name: "Ownboard Carbon Zeus Pro",
      img: "https://www.ownboard.net/cdn/shop/files/Capture00122-2_1024x1024.jpg?v=1708313499",
      price: 1399,
      battery: "Samsung 50S 21700 13S4P 20Ah 936Wh",
      top_speed: 60,
      range: 80,
      weight: 13.0,
      max_load: 150,
    },
    {
      name: "Ownboard W2 PRO",
      img: "https://www.ownboard.net/cdn/shop/products/OwnboardElectricSkateboardW2PROWITH90PUwheels-_4_1200x1200.jpg?v=1702553754",
      price: 579,
      battery: "21700 sP12S 8.0Ah 345.6Wh",
      top_speed: 45,
      range: 30,
      weight: 8.8,
      max_load: 120,
    },
    {
      name: "Ownboard Prometheus Electric",
      img: "https://www.ownboard.net/cdn/shop/files/8C3A4448_1200x1200.jpg?v=1727663452",
      price: 1749,
      battery: "Samsung 50S 12S5P 25Ah 1170Wh",
      top_speed: 60,
      range: 80,
      weight: 20.5,
      max_load: 120,
    },
    {
      name: "Ownboard Mini KT",
      img: "https://www.ownboard.net/cdn/shop/products/8_176367fd-ea6d-46eb-81a8-a533b5035569_800x.jpg?v=1702553690",
      price: 369,
      battery: "18650 & 21700, 2P10S",
      top_speed: 40,
      range: 30.5,
      weight: 7.6,
      max_load: 120,
    },
    {
      name: "Evolve Renegade Diablo",
      img: "https://www.rideevolve.com/cdn/shop/files/Main_White_3.jpg?v=1719381890",
      price: 2299,
      battery: "43.2v - 864Wh - 20Ah - Samsung 50S",
      top_speed: 50,
      range: 50,
      weight: 16.4,
      max_load: 120,
    },
    {
      name: "Evolve Diablo Bamboo Street",
      img: "https://cdn.accentuate.io/8214050406536/1719137335284/Diablo_Bamboo_2in1_Collection.jpg?v=1719137335284",
      price: 1999,
      battery: "Samsung 50S",
      top_speed: 50,
      range: 50,
      weight: 15.3,
      max_load: 120,
    },
    {
      name: "Evolve Stoke X",
      img: "https://www.rideevolve.com/cdn/shop/files/STOKEX-08790-Edit_1024x1024.webp",
      price: 1399,
      battery: "12S2P - 43.2v - 432Wh - 10Ah - Samsung 50S",
      top_speed: 42,
      range: 45,
      weight: 10.5,
      max_load: 100,
    },
    {
      name: "Evolve GTR Bamboo",
      img: "https://www.rideevolve.com/cdn/shop/files/GTR-BAMBOO-CLEAR-82-Edit.jpg?v=1740544513",
      price: 1399,
      battery: "14Ah - 504Wh - 10S4P - 18650 Cells",
      top_speed: 38,
      range: 30,
      weight: 12.1,
      max_load: 100,
    },
  ];
</script>
<div class="main-container">
  <h1>Electric Skateboard Market Analisis</h1>
  <p>
    El mercado de los vehiculos de transporte compactos para uso en ciudades ha incrementado significativamente
    en los últimos años, sin embargo entre estos las patinetas o skateboards electricas parecen no haber 
    recibido la misma atención que otros vehiculos similares como bicicletas electricas o los controversiales 
    scooters electricos o monopatines, a continuación vamos a intentar expandir un poco la visión sobre este
    mercado, analizar las opciónes actuales, un poco argumentar porque se considera que es un mejor medio de transporte
    que las opciones previamente mencinadas y ofrecer un contexto estadístico sobre el uso de estos vehiculos
  </p>

  <h2>Estado Actual del Mercado</h2>

  <h2>Jugadores Principales y valor en el mercado</h2>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th>Marca</th>
          <th>%Mercado</th>
          <th>Especialización</th>
          <th>Rango de Precios</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>Boosted</th>
          <th>~15% (Pre-bancarota)</th>
          <th>Alto rendimiento</th>
          <th>1,000-2,000 USD</th>
        </tr>
        <tr>
          <th>Evolve</th>
          <th>~20%</th>
          <th>Premium & Todo terreno</th>
          <th>1,500-2,000USD</th>
        </tr>
        <tr>
          <th>Meepo</th>
          <th>~12%</th>
          <th>Menor Precio</th>
          <th>400-900USD</th>
        </tr>
        <tr>
          <th>Exway</th>
          <th>~10%</th>
          <th>Funcionalidad Inteligente</th>
          <th>700-1,500USD</th>
        </tr>
        <tr>
          <th>Ownboard</th>
          <th>~8%</th>
          <th>Desempeño Balanceado</th>
          <th>500-1,200USD</th>
        </tr>
        <tr>
          <th>Otros</th>
          <th>~35%</th>
          <th>Marcas de Nicho, kits DIY</th>
          <th>Variable</th>
        </tr>
      </tbody>
    </table>
  </div>
  <h2>Oferta de Mercado</h2>
  <div class="offer-container">
    {#each boards as value}
      <div class="item-container">
        <h4>{value.name}</h4>
        <div class="offer-item">
          <img src={value.img} alt="skate">
        </div>
        <h4>${value.price}</h4>
      </div>
    {/each}
  </div>
  <D3Chart boards: {boards}/>
  <h2>Estadísticas Destacables del Producto</h2>
  <p>
    En esta categoría de vehiculo electrico las características que mas definen el segmento
    y en la que la mayoría de los vendedores se enfocan a la hora de hacer sobresalir su
    producto son las siguientes.
  </p>
  <ul>
    <li>Rango de autonomía con una carga de batería</li>
    <li>Portabilidad</li>
    <li>Velocidad Máxima</li>
    <li>Capacidad todo terreno</li>
    <li>Material de la tabla</li>
  </ul>
  <h3>Gráfica de distribución Precio vs Rango</h3>
  <Scatter skateboards: {boards}/>
  <div class="listas">
    <div class="lista-item">
      <h3>Drives</h3>
      <ul>
        <li>Motores Hub (silenciosos, bajo mantenimiento)</li>
        <li>Belt-Driven (Mas Torque, cadenas reemplazables)</li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Motores (Afecta a el poder y la eficiencia)</h3>
      <ul>
        <li>Motores Sencillos (un solo motor hace todo el empuje)</li>
        <li>Motores Duales (Dos motores realizan el empuje)</li>
        <li>Motores Quad o All-wheel (Un motor en cada una de las cuatro ruedas)</li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Freno</h3>
      <ul>
        <li>Freno Regenerativo (Recupera energía al momento de frenar, tiene impacto en el rango)</li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Batería y Eficiencia</h3>
      <ul>
        <li>Capacidad de Batería (Wh) vs Rango en el mundo real</li>
        <li>Soporte para Recarga Rápida (USB-C, Cargadores Propios)</li>
        <li>Degradación de la batería (Analisis de vida útil)</li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Calidad de Construcción y Materiales</h3>
      <ul>
        <li><strong>Tipos de Tablas:</strong> Bamboo (Flexible), Fibra de Carbono (Ligero), Maple (duradero)</li>
        <li><strong>Trucks y llantas:</strong> Polyuretano (78A-90A), tamaño de llanta (90mm-120mm)</li>
        <li><strong>Resistencia al Agua:</strong>(IP ratings - IP55 vs IP65 vs IP67)</li>
      </ul>
    </div>
  </div>

  <h3>Gráfica de degradación de baterías</h3>
  <Battery />
  <h2>Estadisticas de Usuarios</h2>
  <div class="listas">
    <div class="lista-item">
      <h3>Datos Demográficos</h3>
      <ul>
        <li>
          <strong>Usuarios Principales</strong>
          <ul>
            <li>Profesionales y estudiantes</li>
            <li>Entusiastas (Todo terreno y velocidad)</li>
            <li>Repartidores</li>
          </ul>
        </li>
        <li>
          <strong>Grupo de Edad</strong>
          <ul>
            <li>18-25 (Estudiantes y primerisos)</li>
            <li>26-40 (Profesionales y trabajadores)</li>
            <li>40+ (Hobyistas y uso recreacional)</li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Quejas Comunes</h3>
      <ul>
        <li><strong>Duración de Batería</strong> (Promocionada vs Real)</li>
        <li><strong>Durabilidad</strong> (Agotamiento del motor, grietas en las tablas)</li>
        <li><strong>Ayuda al Consumidor</strong> (Garantías y disponibilidad de repuestos)</li>
        <li><strong>Seguridad</strong> (Roturas espontaneas, desconecciónes de los mandos)</li>
      </ul>
    </div>
    <div class="lista-item">
      <h3>Funcionalidades mejor valoradas</h3>
      <ul>
        <li><strong>Rango</strong>(Prioridad principal)</li>
        <li><strong>Velocidad Y Aceleración</strong> (Entusiastas)</li>
        <li><strong>Portabilidad</strong> (Peso)</li>
        <li><strong>Conectividad con App</strong> (Customización y diagnosticos)</li>
        <li><strong>Resistencia al Agua</strong> (Usabilidad en todo tipo de clima)</li>
      </ul>
    </div>
  </div>
  <h2>Tendencias de la Industria</h2>
  <h3>Analisis de Principales Marcas</h3>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th>Marca</th>
          <th>Fortalezas</th>
          <th>Debilidades</th>
          <th>Oportunidades</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>Evolve</th>
          <th>Premium y Todo terreno</th>
          <th>Costo elevado</th>
          <th>Expandir a transporte Urbano</th>
        </tr>
        <tr>
          <th>Meepo</th>
          <th>Barato y buen desempeño</th>
          <th>Diseños Básicos</th>
          <th>Expansión Global</th>
        </tr>
        <tr>
          <th>Exway</th>
          <th>Funcionalidad Inteligente</th>
          <th>Refacciónes limitadas</th>
          <th>Servicios de Subscripción</th>
        </tr>
      </tbody>
    </table>
  </div>

  <h3>Tendencias Emergentes</h3>
  <ul>
    <li><strong>Integración con IA</strong> (Mantenimiento predictivo, manejo adaptativo)</li>
    <li><strong>Diseño Modular</strong>(Baterías intercambiables, mejoras a los motores)</li>
    <li><strong>Modelos de Subscripción</strong>(servicios de renta para usuarios en las urbes)</li>
    <li><strong>Cambios en regulaciónes</strong> (Limites de velocidad y legalidad en la calle)</li>
  </ul>

  <h3>previsión del futuro</h3>
  <ul>
    <li><strong>Mejora en Baterías</strong> (Estado solido, carga rápida)</li>
    <li><strong>Funcionalidad Autonoma</strong> (Balanceo autonomo, evasión de colisión)</li>
    <li><strong>Consolidación de mercado</strong>(Adquisición de pequeñas marcas por gigantes como Segway)</li>
  </ul>
</div>
<style>
  .table-container {
    display: flex;
    justify-content: center;
    overflow-x: scroll;
  }

  table, thead, tbody, tr, th {
    border: 1px solid white;
  }

  .main-container {
    margin: 5rem 1rem 0 1rem;
    overflow-x: hidden;
  }

  .listas {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    align-items: center;
  }

  .lista-item {
    border: 1px solid white;
    border-radius: 6px;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    padding: 1rem;
    margin: 1rem 0;
  }

  .offer-container {
    width: 100%;
    align-items: center;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    display: flex;
  }

  .item-container {
    display: flex;
    flex-direction: column;
    align-items: center;

    & h4 {
      color: white;
    }
  }

  .offer-item {
    position: relative;
    flex: 0 0 auto;
    margin: 0 1rem;
    width: 200px;
    height: 200px;
    background-color: lightgray;
    flex-shrink: 0;
    border-radius: 5px;
    scroll-snap-align: start;
    display: flex;
    justify-content: center;
    
    & img {
      height: 100%;
      width: 100%;
      object-fit: cover;
      display: block;
      border-radius: 5px;
    }
  }

  @media (max-width: 500px) {
    .table-container {
      display: block;
    }

    .main-container {
      margin-top: 1rem;
      overflow-x: scroll;
    }

    .listas {
      display: block;
    }

    .lista-item {
      display: block;
    }
  }
</style>
