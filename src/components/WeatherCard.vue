<template>
  <div class="card" v-bind:class="{'appeared': active}">
    <div class="location">
      {{ address }}
    </div>
    <div class="temperature">
      <img src="@/assets/thermometer.svg" />
      {{ temperature.toFixed(2) }}
    </div>
    <div class="weather">
      {{ weather }}
    </div> 
  </div>
</template>

<script>
export default {
  props: {
    temperature: {
      type: Number,
      default: 0
    },
    weather: {
      type: String,
      default: ""
    },
    address: {
      type: String,
      default: ""
    },
    active: {
      type: Boolean,
      default: false
    }
  }
};
</script>

<style lang="less" scoped>
#app {
  overflow-y: hidden;
}
.card {
  position: absolute;
  top: 5rem;
  background: #fff;
  left: 0;
  right: 0;
  bottom: 0;
  height: 120%;
  padding: 1rem;
  background: rgb(195,34,79);
  background: linear-gradient(0deg, rgba(195,34,79,1) 0%, rgba(253,85,45,1) 100%);
  z-index:-1;
  -webkit-transition: all cubic-bezier() 250ms;
  transition: all linear 250ms;
  opacity: 0;
  &.appeared {
    opacity: 1;
    z-index: 99;
    -webkit-transform: translateY(-5rem);
    transform: translateY(-5rem);
    -webkit-transition: all linear 500ms;
    transition: all linear 500ms;
  }
  * {
    text-align: center;
    color: #fff
  }
  .location {
    font-size: 0.875rem;
    max-width: 75%;
    margin: 0px auto;
  }
  .temperature {
    margin-top: 2rem;
    font-size: 7rem;
    font-weight: 800;
    text-shadow: 0px 4px 8px rgba(91, 91, 91, 0.3);
    line-height: 1;
    img {
      max-width: 35%;
      margin: 0px auto;
    }
  }
  .weather {
    text-transform: capitalize;
  }
}

</style>
