<template>
  <div id="app">
    <div v-for='(list, index)  in original_lists' class="col-xs-3">
      <h6> {{ list.name }} </h6>
      <hr />

      <div v-for='(card, index) in list.cards' class="card card-body">
        {{ card.name }}
      </div>

      <div class="card-form">
        <textarea v-model="messages[list.id]" class="form-control"> </textarea>
        <button @click='submitMessages(list.id)' class="btn btn-primary"> Save </button>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  props: ['original_lists'],
  data() {
    return {
      messages: {}
    }
  },
  methods: {
    submitMessages(list_id) {
      console.log(this.messages[list_id])
    }
  }

}
</script>

<style>
p {
  font-size: 2em;
  text-align: center;
}

.card-body {
  border: 1px solid black;
  padding: 10px 3px;
  text-align: center;
}

.card-form {
  margin-top: 15px;
}
</style>
