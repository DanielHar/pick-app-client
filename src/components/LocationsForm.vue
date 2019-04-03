<template>
  <v-form>
    <v-container>
      <v-layout row wrap>
        <v-flex xs12 sm6 md3>
          <v-text-field
            v-model="startingPoint"
            label="Starting point"
          ></v-text-field>
        </v-flex>
      </v-layout>
      <v-layout row wrap v-for="i in showPoints" :key="i - 1">
        <v-flex xs12 sm6 md3>
          <v-text-field
            :label="'point ' + i"
            v-model="points[i - 1]"
          ></v-text-field>
        </v-flex>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs12 sm6 md3>
          <v-text-field
            v-model="finishPoint"
            label="Finish point"
          ></v-text-field>
        </v-flex>
        <v-flex xs12 sm6 md3 v-if="showPoints < 4">
          <v-btn fab dark color="indigo" v-on:click="addPoint">
            <v-icon dark>add</v-icon>
          </v-btn>
        </v-flex>
      </v-layout>
      <v-btn color="success" class="ml-0" v-on:click="sendRequest">Send Request</v-btn>
      <span v-if="instructions != ''">{{instructions}}</span>
    </v-container>
  </v-form>
</template>

<script>
  import Axios from 'axios';
  export default {
    data: () => ({
      startingPoint: "",
      finishPoint: "",
      points: ["", "", "", ""],
      showPoints: 1,
      instructions: ""
    }),
    methods: {
      addPoint() {
        if (this.showPoints < 4) this.showPoints++;
      },
      sendRequest() {
        const params = {
          startPoint: this.startingPoint,
          endPoint: this.finishPoint,
          points: []
        }

        this.points.map(point => {
          if(point != "") params.points.push(point)
        });

        Axios.get('/instructions', {
          params: params
        }).then(response => {
          this.instructions = response.data;
          this.startingPoint = "";
          this.finishPoint = "";
          this.showPoints = 1;
          this.points = ["", "", "", ""];
        });
      }
    }
  }
</script>