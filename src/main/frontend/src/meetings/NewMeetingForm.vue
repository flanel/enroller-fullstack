<template>
  <div>
    <form @submit.prevent="addNewMeeting()" v-if="adding">
      <h3>Dodaj nowe spotkanie</h3>
      <label>Nazwa</label>
      <input type="text" v-model="newMeeting.name">
      <label>Opis</label>
      <textarea v-model="newMeeting.description"></textarea>
      <button>Dodaj</button>
      <span class="error" v-if="error">Spotkanie musi mieć nazwę!</span>
    </form>
    <button @click="adding = true" v-else>Dodaj nowe spotkanie</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        newMeeting: {participants: []},
        adding: false,
        error: false
      };
    },
    methods: {
      addNewMeeting() {
        this.error = false;
        if (this.newMeeting.name) {
          this.$emit('added', this.newMeeting);
          this.newMeeting = {participants: []};
          this.adding = false;
          this.$http.post('meetings', newMeeting).then(() => {
            this.success('Spotkanie zostało dodane.');
          })
                  .catch(response => this.failure('Błąd przy dodawaniu spotkania. Kod odpowiedzi: ' + response.status));

        } else {
          this.error = true;
        }
      }
    },
    mounted() {
      const name = localStorage.getItem('name');
      const desctiption = localStorage.getItem('desctiption');
    }
  }
</script>

<style scoped>
  .error {
    color: #F00;
  }
</style>