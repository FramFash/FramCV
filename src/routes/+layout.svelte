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
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    background: linear-gradient(to bottom, rgba(255,255,255,0.15) 0%, rgba(0,0,0,0.15) 100%), radial-gradient(at top center, rgba(255,255,255,0.40) 0%, rgba(0,0,0,0.40) 120%) #989898;
    background-blend-mode: multiply,multiply;
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
      text-decoration: none;
      border: 1px solid lightgray;
      border-radius: 10px;
      padding: 0.5rem;
      box-shadow: 0 0 1px 1px white;
    }
  }

  @media (max-width: 500px) {
    header {
      margin-top: 30px;
      position: relative;
    }

    .h-center {
      width: 100%;
    }
    .links {
      justify-content: space-around;
    }
  }

</style>
