<template>
  <div class="notes">
    <v-container>
      <v-row>
        <v-btn
          class="ma-2"
          elevation="2"
          v-if="createNote"
          @click="createBtn(false)"
        >
          <v-icon dark> mdi-minus</v-icon>
        </v-btn>
        <v-btn class="ma-2" elevation="2" v-else @click="createBtn(true)">
          <v-icon dark> mdi-plus</v-icon>
        </v-btn>
        <h1>Post It Page</h1>
      </v-row>
    </v-container>

    <!-- Create Note Card -->
    <v-container fluid>
      <v-row>
        <div class="newNote" v-if="createNote">
          <AddNote></AddNote>
        </div>

        <!--- Cards --->
        <template v-for="note in notelist" :key="note.id">
          <v-col md="3" class="mb-4">
            <form @submit.prevent="update(note._id)">
              <v-card
                class="pa-md-4 mx-lg-auto cards"
                max-width="300"
                elevation="2"
                v-if="notelist.length"
              >
                <p hidden :dtl="note._id">{{ note._id }}</p>
                <input type="text" v-model="note.title" />
                <p></p>
                <textarea
                  rows="3"
                  v-model="note.content"
                  name="note.contents"
                ></textarea>

                <div class="text-center">
                  <v-btn text color="primary" size="small">
                    <router-link
                      :id="note._id"
                      :to="{
                        name: 'details',
                        params: {
                          id: note._id,
                          title: note.title,
                          content: note.content,
                        },
                      }"
                    >
                      More
                      <v-icon right> mdi-arrow-right </v-icon>
                    </router-link>
                  </v-btn>
                  <DeleteBtn :id="note._id"></DeleteBtn>
                </div>
              </v-card>
            </form>
          </v-col>
        </template>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import DeleteBtn from "../components/DeleteBtn";
import AddNote from "../components/AddNote";

export default {
  name: "notes",
  components: { AddNote, DeleteBtn },
  props: ["id"],

  data: () => ({
    createNote: false,
    notelist: [],
  }),

  // -- Get All Notes
  async created() {
    const res = await fetch("http://5.135.119.239:3090/notes");
    const data = await res.json();
    this.notelist = data.notes;
    //location.reload();
  },

  methods: {
    createBtn(createNote) {
      this.createNote = createNote;
      //this.newNote = ""
    },
    // --- Get Notes By Id
    async getId(id) {
      const res = await fetch("http://5.135.119.239:3090/notes/" + id);
      const data = await res.json();
      this.notelist = data;
      console.log(data);
    },
  },
};
</script>
<style scoped>
.cards {
  background: #fffdd0;
  font-size: 20px;
}
.newNote {
  margin: 0 12px;
}

.noteblock {
  background: #faf0e6;
}
</style>
