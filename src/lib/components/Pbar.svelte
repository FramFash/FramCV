<script lang='ts'>
  export let progress;
</script>

<div class="bar" style="--fill-progress: {progress}%">
  <div class="prog"></div>
</div>

<style>
  .bar {
    margin: auto 0;
    width: 80%;
    height: 20px;
    margin-left: 0.5rem;
    background-color: gray;
    border-radius: 5px;
  }

  .prog {
    width: var(--fill-progress);
    height: 20px;
    background-image: linear-gradient(45deg, #ff9a9e 0%, #fad0c4 99%, #fad0c4 100%);
    border-radius: 5px;
    transition: 0.5s;
    background-size: 200% auto;
  }

  .prog:hover {
    background-position:  right center;
  }
</style>
