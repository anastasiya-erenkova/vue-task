<template lang="html">
  <div class="messages">
    <div class="messages__head">
      <h2 class="messages__title">Questions Messenger</h2>
      <select class="messages__select">
        <option>All Questions</option>
        <option>Not All Questions</option>
      </select>
    </div>
    <div class="messages__body">
      <div class="message" v-for="message in messages" v-if="message.category == activeCategory">
        <p class="message__text">{{message.text}}</p>
        <p class="message__date">{{message.date}}</p>
      </div>
    </div>
    <div class="messages__new">
      <textarea v-model="newMessage.text" class="message__textarea"></textarea>
      <button class="message__btn btn" type="button" @click="addMessage">Отправить</button>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  props: ["categories", "messages", "activeCategory"],
  data() {
    return {
      newMessage: {}
    };
  },
  methods: {
    addMessage: function() {
      if (!this.newMessage.text) {
        return;
      }

      const optDate = {
        day: "numeric",
        month: "long",
        hour: "numeric",
        minute: "numeric"
      };

      this.newMessage.date = new Date().toLocaleString("ru", optDate);

      this.newMessage.category = this.activeCategory;

      this.messages.push(this.newMessage);
      this.newMessage = {};
      this.$emit("saveMessages", this.messages);
    }
  }
};
</script>