<script>
  import { base } from "$app/paths";
</script>
<div class="main-container">
  <a href="showcase/cyberinfo/" class="project">
    <h3>Datos Visibles</h3>
    <p>
      esta pagina revela la información que está accesible a el buscador y por resultado a el creador de
      la pagina, es meramente informativa y no almacena ningun tipo de información.
    </p>
  </a>
  <a href="showcase/otro/" class="project">
    <h3>otro</h3>
    <p>
      esta pagina revela la información que está accesible a el buscador y por resultado a el creador de
      la pagina, es meramente informativa y no almacena ningun tipo de información.
    </p>
  </a>
</div>
<style>
  .main-container {
    margin: 5rem 1rem 1rem 1rem;
    color: white;
    display: grid;
    grid-template-columns: 50% 50%;
  }
  .project {
    border: 1px solid white;
    border-radius: 10px;
    margin: 1rem;
    padding: 0.5rem;
    text-decoration: none;
    color: black;
    background-image: linear-gradient(to right, #757F9A 0%, #D7DDE8  51%, #757F9A  100%);
    text-transform: uppercase;
    transition: 0.5s;
    background-size: 200% auto;
  }
  .project:hover {
      background-position: right center; /* change the direction of the change here */
      text-decoration: none;
  }
</style>
