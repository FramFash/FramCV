<script>
  import { base } from "$app/paths";
</script>

<div class="main-container">
  <div class="top-info">
    <div class="basic-data">
      <div class="row">
        <img src={`${base}/images/email.png`} alt="icon">
        <h5>fram.tid.fash@gmail.com</h5>
      </div>
      <div class="row">
        <img src={`${base}/images/whatsapp.png`} alt="icon">
        <h5>+52-55-5417-8404</h5>
      </div>
      <div class="row">
        <img src={`${base}/images/location.png`} alt="icon">
        <h5>Mexico City, Mexico</h5>
      </div>
    </div>
  </div>
</div>
<style>
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.top-info {
  display: flex;
  justify-content: space-around;
  margin-top: 10rem;
  border-radius: 5px;
  box-shadow: 0 0 10px 2px #F05F57;
  background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
}

.basic-data {
  grid-column: 2 / 3;
  display: flex;
  flex-direction: column;
  align-items:flex-start;
}

.row {
  grid-column: 1 / 3;
  display: flex;
  align-items: center;

  & img {
    margin-left: 0.5rem;
    width: 30px;
  }

  & * {
    margin: 0.5rem;
  }
}

</style>
