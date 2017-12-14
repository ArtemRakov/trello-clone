<template>
  <div id="app">
    <div v-for='list in original_lists' class="col-xs-3">
      <h6> {{ list.name }} </h6>
      <hr />

      <div v-for='(card, index) in list.cards' class="card card-body">
        {{ card.name }}
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: ['original_lists'],


}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}

.card {
  border: 5px solid grey;
}
</style>
