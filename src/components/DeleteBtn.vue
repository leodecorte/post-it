<template>
  <v-btn @click="deleteNote" class="ma-2" color="red" white size="small">
    <v-icon white> mdi-delete </v-icon>
  </v-btn>
</template>

<script>
export default {
  name: "DeleteBtn",
  props: ["id"],

  methods: {
    deleteNote() {
      const deleteData = async () => {
        const response = await fetch(
          "http://5.135.119.239:3090/notes/" + this.id,
          {
            method: "DELETE",
            headers: {
              "Content-Type": "application/json",
            },
          }
        );
        const data = await response.json();
        console.log(data);
        location.reload();
      };
      deleteData();
    },
  },
};
</script>