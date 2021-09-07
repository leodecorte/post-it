<template>
  <v-container>
    <h1>Update Your Post-It</h1>
    <v-col>
      <form @submit.prevent="update(this.$route.params.id)">
        <v-card class="pa-md-4 mx-lg-auto cards" max-width="350" elevation="2">
          <input
            @keyup.enter="update(this.$route.params.id)"
            v-model="this.$route.params.title"
          />
          <p></p>
          <textarea
            rows="3"
            v-model="this.$route.params.content"
            name="note.contents"
            @keyup.enter="update(this.$route.params.id)"
          ></textarea>
          <div class="text-center">
            <v-btn
              text
              color="primary"
              size="small"
              value="submit"
              @click="update(this.$route.params.id)"
              ><router-link :to="{ name: 'Home' }">
                Back
                <v-icon right> mdi-arrow-left </v-icon>
              </router-link>
            </v-btn>
          </div>
        </v-card>
      </form>
    </v-col>
  </v-container>
</template>

<script>
export default {
  props: ["id"],

  data: () => ({}),

  methods: {
    update(id) {
      const updatePost = {
        title: this.$route.params.title,
        content: this.$route.params.content,
      };

      const putData = async () => {
        const response = await fetch("http://5.135.119.239:3090/notes/" + id, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(updatePost),
        });

        const data = await response.json();
        console.log(data);
      };
      putData();
    },
  },
};
</script>
<style>
.cards {
  font-size: 25px;
}
</style>
