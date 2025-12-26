<template>
  <div class="container p-0">
    <div class="d-flex">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">Tuesday</h2>
          <p class="text-light date">date</p>
          <small>time</small>
          <h2 class="place"><i class="fas fa-location"></i> Rio <small>Country</small></h2>
          <div class="temp">
            <h1 class="weather-temp">19&deg;</h1>
            <h2 class="text-light">description</h2>
          </div>
        </div>
      </div>
      <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Sea Level</th>
              <td>100</td>
            </tr>
            <tr>
              <th>Sea Level</th>
              <td>100</td>
            </tr>
            <tr>
              <th>Sea Level</th>
              <td>100</td>
            </tr>
          </tbody>
        </table>
        <div id="chg_btn_div" class="d-flex justify-content-center m-3">
          <form action="">
            <input type="button" value="Change Location" class="btn change-btn btn-primary">
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'theWeather',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body {
    background-color: #343d4b;
  }
  .weather-temp {
    margin: 0;
    font-size: 4em;
    font-weight: 700;
  }
  h2.mb-1.day {
    font-size: 3rem;
    font-weight: 400;
  }
  .card {
    border-radius: 20px;
    color: #ffffff;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
