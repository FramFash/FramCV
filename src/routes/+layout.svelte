<script>
  import { base } from '$app/paths';
</script>
<header>
  <div class="h-center">
    <div class="links">
      <a href={`${base}/`}>home</a>
      <a href={`${base}/bio`}>bio</a>
      <a href={`${base}/showcase`}>showcase</a>
      <a href={`${base}/contact`}>contact</a>
    </div>
  </div>
</header>
<slot/>
<style>
  :global(body) {
    margin: 0;
    padding: 0;
    background: #1A1A1A;
    color: white;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  }

  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    padding: 0.5rem 1rem;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);

  }

  .h-center {
    width: 40%;
    height: 50px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .links {
    width: 100%;
    display: flex;
    justify-content: space-between;
    & a {
      color: white;
    }
  }

  @media (max-width: 500px) {
    .h-center {
      width: 100%;
    }
    .links {
      justify-content: space-around;
    }
  }

</style>
