<template>
  <div>
    <br />
    <br />
    <v-card color="info" dark outlined>
      <hr />
      <center>
        <h1>Unread Requests</h1>
      </center>
      <hr />
    </v-card>

    <v-expansion-panels inset focusable>
      <RequestCard
        v-for="(request, index) in requests"
        :request="request"
        :key="index"
        @remove="removeItem(request)"
      />
    </v-expansion-panels>
  </div>
</template>
<script>
import RequestCard from "../modules/tibs/RequestContainer.vue";
import { getUnread } from "../actions/requestAxios.js";
// import io from "socket.io-client";
// var socket = io.connect("http://localhost:3232");
export default {
  components: {
    RequestCard
  },
  data() {
    return {
      sample: "sample",
      username: "redgie",
      requests: []
    };
  },
  methods: {
    removeItem(request) {
      this.requests.splice(this.requests.indexOf(request), 1);
    }
  },
  mounted() {
    getUnread()
      .then(data => (this.requests = data.data))
      .catch(err => alert(err));
  }
};
</script>
