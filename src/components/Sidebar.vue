<template lang="html">
  <div class="sidebar">
    <div class="sidebar__head">
      <div class="user">
        <div class="user__img" :style='{ backgroundImage: "url(http://gloria-mur.ru/wp-content/uploads/2017/05/avatar1-740x463.jpg)", }'></div>
        <div class="user__inner">
            <p class="user__name">{{ user.name }}</p>
            <p class="user__status">{{ user.status }}</p>
        </div>
      </div>
      <button title="Добавить категорию" class="category__add" type="button" @click="openAddCategory=true">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 11 11">
          <g transform="translate(-4231.65 -3105)">
            <rect width="2.3" height="11" transform="translate(4236 3105)"/>
            <rect width="2.3" height="11" transform="translate(4242.65 3109.35) rotate(90)"/>
          </g>
        </svg>
      </button>
    </div>
    <div class="sidebar__body category">
      <p class="category__title">Messages</p>
      <p class="category__subtitle">history</p>
      <ul>
          <li class="category__item" v-for="category in categories" 
              :class="category == activeCategory ? 'is-active': '' "
              @click="$emit('changeCategory', category)">{{ category }}</li>
          <li class="category__field" v-if="openAddCategory">
            <input v-model="newCategory" class="category__inp" />
            <button type="button" class="category__btn btn" @click="addCategory">Добавить</button>
          </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import { Component } from "vue-property-decorator";
export default {
  props: ["categories", "activeCategory"],
  data() {
    return {
      // categories: ["My Questions", "Messenger", "Communuti QA", "FAQ"],
      user: {
        img: "/img/user.jpg",
        name: "David Hill",
        status: "online"
      },
      openAddCategory: false,
      newCategory: null
    };
  },

  methods: {
    addCategory: function() {
      if (!this.newCategory) {
        return;
      }

      this.categories.push(this.newCategory);
      this.newCategory = "";
      this.$emit("saveCategories", this.categories);

      this.openAddCategory = false;
    }
  }
};
</script>