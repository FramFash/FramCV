<script lang='ts'>
  export let progress;
</script>

<div class="bar" style="--fill-progress: {progress}%">
  <div class="prog"></div>
</div>

<style>
  .bar {
    margin: auto;
    width: 80%;
    height: 20px;
    margin-left: 1rem;
    background-color: gray;
    border-radius: 5px;
  }

  .prog {
    width: var(--fill-progress);
    height: 20px;
    background-image: linear-gradient(45deg, #ff9a9e 0%, #fad0c4 99%, #fad0c4 100%);
    border-radius: 5px;
  }
</style>
