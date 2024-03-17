<script>
  export let year;
  export let city;
  export let event;
  export let medal;
  export let left = true;
</script>

<div class="container" class:left class:right={!left}>
  <div class="content">
    <h2>{year}</h2>
    <h2>{city}</h2>
    <h2>{event}</h2>
    <h2>{medal}</h2>
  </div>
</div>

<style>
  .container {
    padding: 10px 40px;
    position: relative;
    background-color: inherit;
    width: 39%;
  }

  .container::after {
    content: '';
    position: absolute;
    width: 25px;
    height: 25px;
    right: -17px;
    background-color: white;
    border: 4px solid #ff9f55;
    top: 15px;
    border-radius: 50%;
    z-index: 1;
  }

  .left {
    left: 0;
  }

  .right {
    left: 50%;
  }
  .left::before {
    content: ' ';
    height: 0;
    position: absolute;
    top: 22px;
    width: 0;
    z-index: 1;
    right: 30px;
    border: medium solid white;
    border-width: 10px 0 10px 10px;
    border-color: transparent transparent transparent white;
  }

  .right::before {
    content: ' ';
    height: 0;
    position: absolute;
    top: 22px;
    width: 0;
    z-index: 1;
    left: 30px;
    border: medium solid white;
    border-width: 10px 10px 10px 0;
    border-color: transparent white transparent transparent;
  }

  .right::after {
    left: -16px;
  }

  .content {
    padding: 20px 30px;
    background-color: white;
    position: relative;
    border-radius: 6px;
  }

  @media screen and (max-width: 600px) {
    .container {
      width: 100%;
      padding-left: 70px;
      padding-right: 25px;
    }

    .container::before {
      left: 60px;
      border: medium solid white;
      border-width: 10px 10px 10px 0;
      border-color: transparent white transparent transparent;
    }

    .left::after,
    .right::after {
      left: 15px;
    }

    .right {
      left: 0%;
    }
  }
</style>
