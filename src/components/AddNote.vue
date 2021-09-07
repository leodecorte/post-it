<template>
  <!--- Card Add --->
  <form @submit.prevent="createPost">
    <v-card class="pa-md-4 mx-lg-auto cards" max-width="300" elevation="2" tile>
      <p>Create your note</p>
      <input type="text" id="title" placeholder="title" v-model="title" />

      <textarea
        rows="3"
        name="note.contents"
        placeholder="content"
        v-model="content"
      ></textarea>

      <div class="text-center">
        <v-btn type="submit" class="ma-2" color="primary" dark size="small">
          Add Note
        </v-btn>
      </div>
    </v-card>
  </form>
</template>

<script>
export default {
  methods: {
    async createPost() {
      const newPost = { title: this.title, content: this.content };
      // POST request using fetch with async/await
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(newPost),
      };
      const response = await fetch(
        "http://5.135.119.239:3090/notes",
        requestOptions
      );
      const data = await response.json();
      this.newPost = data.id;
      console.log(newPost);
      //this.newPost = ""
      location.reload();
    },
  },
};
</script>
<style scoped>
.cards {
  margin: 5px;
  background: #fffdab;
  font-size: 18px;
}
</style>