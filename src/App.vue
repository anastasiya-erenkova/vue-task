<template>
  <main class="main">
    <Sidebar
      :categories="categories"
      :activeCategory="activeCategory"
      v-on:saveCategories="saveCategories"
      v-on:changeCategory="changeCategory"
    />
    <Messages
      :categories="categories"
      :activeCategory="activeCategory"
      :messages="messages"
      v-on:saveMessages="saveMessages"
    />
  </main>
</template>

<script>
import Vue from "vue";
import { Component } from "vue-property-decorator";
import Sidebar from "./components/Sidebar.vue";
import Messages from "./components/Messages.vue";

export default {
  components: {
    Sidebar,
    Messages
  },
  data() {
    return {
      categories: ["My Questions", "Messenger", "Communuti QA", "FAQ"],
      activeCategory: null,
      messages: []
    };
  },
  mounted() {
    this.messages = [
      {
        category: this.categories[0],
        date: "17 июня, 12:44",
        text:
          "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean consequat sapien erat, sed pretium urna tincidunt rutrum. Donec mattis maximus justo, vel condimentum augue tristique molestie. Donec ullamcorper maximus aliquam. Interdum et malesuada "
      },
      {
        category: this.categories[0],
        date: "18 июня, 12:44",
        text:
          "consectetur adipiscing elit. Aenean consequat sapien erat, sed pretium urna tincidunt rutrum. Donec mattis maximus justo, vel condimentum augue tristique molestie. Donec ullamcorper maximus aliquam. Interdum et malesuada "
      },
      {
        category: this.categories[1],
        date: "18 июня, 22:44",
        text:
          "Aenean consequat sapien erat, sed pretium urna tincidunt rutrum. Donec mattis maximus justo, vel condimentum augue tristique molestie. Donec ullamcorper maximus aliquam. Interdum et malesuada "
      }
    ];

    if (localStorage.getItem("categories")) {
      try {
        this.categories = JSON.parse(localStorage.getItem("categories"));
      } catch (e) {
        localStorage.removeItem("categories");
      }
    }

    if (localStorage.getItem("messages")) {
      try {
        this.messages = JSON.parse(localStorage.getItem("messages"));
      } catch (e) {
        localStorage.removeItem("messages");
      }
    }

    if (localStorage.getItem("messages")) {
      try {
        this.activeCategory =
          localStorage.getItem("activeCategory") || this.categories[0];
      } catch (e) {
        localStorage.removeItem("activeCategory");
      }
    }
  },

  methods: {
    saveCategories: function(categories) {
      const parsedCategories = JSON.stringify(this.categories);
      localStorage.setItem("categories", parsedCategories);
    },
    changeCategory: function(category) {
      this.activeCategory = category;
      localStorage.setItem("activeCategory", category);
    },
    saveMessages: function(messages) {
      const parsedMessages = JSON.stringify(this.messages);
      localStorage.setItem("messages", parsedMessages);
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/main.scss";
</style>