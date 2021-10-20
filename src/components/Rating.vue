<template>
  <div className="rating-container">
      <label className="rating-container__star" v-for="(item, key) in [...Array(5)]" :key="key">
        <input type="radio" v-model="rate" :value="key+1" />
        <font-awesome-icon :icon="appIcon" style="color: rgb(192,192,192)" v-bind:class="[(key+1 < rate || key+1 === rate) ? activeClass : '' ]" />
      </label >
  </div>
</template>

<script>
import { FontAwesomeIcon  } from '@fortawesome/vue-fontawesome';
import { faStar } from '@fortawesome/free-solid-svg-icons';

export default {
  name: 'Rating',
  data (){
    return {
      rate: 0,
      activeClass: "active"
    }
  },
  components: {
    FontAwesomeIcon
  },
  computed: {
    appIcon () {
      return faStar
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.rating-container {
  &__star{
    input[type=radio]{
      display: none;
    }
    .active {
      color: #000 !important
    }
  }
}
</style>
