<template>
  <v-container fluid grid-list-md text-xs-center>
    <v-layout flex>
      <v-flex xs12>
        <v-card>
        <v-card-title v-if="!noHeader" primary-title>
          <h4 class="headline mb-0">Flaws</h4>
        </v-card-title>
          <v-card-text>
            <v-layout row wrap v-for="(flaw, index) in character.flaws" :key="'flaw'+index">
                <v-flex xs9>
                <v-text-field label="Flaw" v-model="flaw.name" @input="updateflaw(index, flaw)"></v-text-field>
                </v-flex>
                <v-flex xs3>
                <v-btn flat color="primary" dark @click="removeFlaw(index)"><i class="material-icons">delete</i></v-btn>
                </v-flex>
            </v-layout>
          </v-card-text>
          <v-card-actions>
            <v-btn flat color="primary" dark @click="addFlaw()">Add flaw</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex> 
    </v-layout> 
  </v-container>
</template>

<script>
export default {
  model: {
    prop: "character"
  },
  props: ["character", "noHeader"],
  data() {
    return {};
  },
  methods: {
    save: function() {
      this.$eventHub.$emit("autoSave");
    },
    addFlaw: function() {
      this.character.flaws.push({
        name: ""
      });
      this.save();
    },
    removeFlaw: function(index) {
      this.character.flaws.splice(index, 1);
      this.save();
    },
    updateflaw: function(index, flaw) {
      this.character.flaws[index] = flaw;
      this.save();
    }
  },
  components: {}
};
</script>
