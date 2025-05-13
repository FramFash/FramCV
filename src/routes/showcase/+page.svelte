<script>
  import { base } from "$app/paths";
</script>
<div class="main-container">
  <a href="showcase/cyberinfo/" class="project">
    <h3>Datos Visibles</h3>
    <p>
      Esta pagina revela la información que está accesible a el buscador y por resultado a el creador de
      la pagina, es meramente informativa y no almacena ningun tipo de información.
    </p>
  </a>
  <a href="showcase/estadisticas/" class="project">
    <h3>Estadisticas de Patinetas Electricas</h3>
    <p>
      Una pagina de ejemplo de analisis estadístico de un producto, en este caso se analiza la oferta
      de producto, sus capacidades técnicas y se trata de llegar a una evaluación logica de las mejores opciones
      en el mercado
    </p>
  </a>
  <a href="showcase/otro/" class="project">
    <h3>Work in progress</h3>
    <p>
    </p>
  </a>
  <a href="https://framfash.github.io/digimon_tcg_io" class="project">
    <h3>Juego de Cartas</h3>
    <p>
      Es un pequeño proyecto personal que lee de una base de datos existente la información de las cartas existentes
      de un juego de cartas japones, y almacena información de las cartas seleccionadas como favoritas u obtenidas.
    </p>
  </a>
</div>
<style>
  .main-container {
    margin: 5rem 1rem 1rem 1rem;
    color: white;
    display: grid;
    padding: 1rem;
    gap: 1rem;
    grid-template-columns: 50% 50%;
  }
  .project {
    border: 1px solid white;
    border-radius: 5px;
    padding: 0.5rem;
    text-decoration: none;
    color: black;
    background-image: linear-gradient(to right, #757F9A 0%, #D7DDE8  51%, #757F9A  100%);
    transition: 0.5s;
    background-size: 200% auto;
  }
  .project:hover {
      background-position: right center; /* change the direction of the change here */
      text-decoration: none;
  }

  @media (max-width: 500px) {
    .main-container {
      margin: 1rem;
    }
    .project {
      margin: 0.5rem;
      font-size: 0.6rem;
    }
  }
</style>
