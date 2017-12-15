<template>
  <draggable :options="{group: 'lists'}" class='row dragArea' @end='listMoved'>
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
  </draggable>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  components: { draggable },
  props: ['original_lists'],
  data() {
    return {
      messages: {},
      lists: this.original_lists
    }
  },
  methods: {
    submitMessages(list_id) {
      var data = new FormData
      data.append('card[list_id]', list_id)
      data.append('card[name]', this.messages[list_id])

      Rails.ajax({
        url: '/cards',
        type: 'POST',
        data: data,
        dataType: 'json',
        success: (data) => {
          const index = this.lists.findIndex(item => item.id === list_id)
          this.lists[index].cards.push(data)
          this.messages[list_id] = undefined
        }
      })
    },
    listMoved(event) {
      var data = new FormData
      data.append('list[position]', event.newIndex + 1)

      Rails.ajax({
        url: `/lists/${this.lists[event.oldIndex].id}/move`,
        type: 'PATCH',
        data: data,
        dataType: 'json'
      })
    }
  }

}
</script>

<style>
p {
  font-size: 2em;
  text-align: center;
}

.dragArea {
  min-height: 20px;
}

.card-body {
  border: 1px solid black;
  padding: 10px 3px;
  text-align: center;
  margin: 10px 0;
}

.card-form {
  margin-top: 15px;
}
</style>
