<template>
  <div class="container">
    <h1>First draft of the Chat!</h1>
    <div class="grid_container">
      <chat
        @emit-send="sendMessage()"
        :textMessage.sync="message"
        :conversation="conversation"
      ></chat>
      <toolbox :concatenateToMessage="concatenateToMessage"></toolbox>
    </div>
    <!-- <chat @emit-send="sendMessage()" :textMessage.sync="message" :conversation="conversation"></chat> -->
  </div>
</template>

<script lang="ts">
import Chat from "./../components/chat/chat_interface.vue";
import Toolbox from "./../components/toolbox/toolbox_interface.vue";

import { conversation } from "./../test/conversation";

import Vue from "vue";

export default Vue.extend({
  data() {
    return {
      message: "",
      conversation,
    };
  },
  components: {
    Chat,
    Toolbox,
  },
  methods: {
    sendMessage: function() {
      if (this.message != "") {
        conversation.push({ sender: "user", text: this.message });
        console.log("I sent: " + this.message);
        this.message = "";
      }
      // this.message += "ciao";
    },
    concatenateToMessage: function(newPiece: string) {
      this.message += " " + newPiece;
    },
  },
});
</script>
<style scoped>
.container {
  height: 88vh;
  overflow: hidden;
}

.grid_container {
  display: inline-grid;
  grid-template-columns: 30% 70%;
  /* grid-template-rows: auto; */
  grid-gap: 10px;
  /* background-color: #2196f3; */
  height: 90%;
  width: 80%;
  /* display: flex; */
}
</style>
