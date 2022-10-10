<template>
  <p>Reaction Time - {{ score }} ms</p>
  <p class="rank">{{ rank }}</p>
</template>

<script>
export default {
  props: ["score"],

  mounted() {
    if (this.score < 270) {
      this.rank = "Ninja Fingers";
    } else if (this.score < 420) {
      this.rank = "Rapid Reflexes";
    } else {
      this.rank = "Snail pace ...";
    }
  },

  data() {
    return {
      rank: null,
    };
  },
};
</script>

<style>
.rank {
  font-size: 1.4em;
  color: #0faf87;
  font-weight: bold;
}
</style>