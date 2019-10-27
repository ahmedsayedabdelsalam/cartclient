<template>
  <nav class="navbar is-white">
    <div class="container">
      <div class="navbar-brand">
        <nuxt-link :to="{ name: 'index' }" class="navbar-item">Cart</nuxt-link>
      </div>

      <div class="navbar-menu">
        <template v-for="category in categories">
          <template v-if="category.children.length">
            <div class="navbar-item is-hoverable has-dropdown" :key="category.slug">
              <nuxt-link
                class="navbar-link"
                :to="{name: 'categories-slug', params: {slug: category.slug}}"
              >{{category.name}}</nuxt-link>
              <div class="navbar-dropdown">
                <nuxt-link
                  class="navbar-item"
                  :to="{name: 'categories-slug', params: {slug: child.slug}}"
                  v-for="child in category.children"
                  :key="child.slug"
                >{{child.name}}</nuxt-link>
              </div>
            </div>
          </template>
          <template v-else>
            <nuxt-link
              class="navbar-item"
              :to="{name: 'categories-slug', params: {slug: category.slug}}"
              :key="category.slug"
            >
              {{category.name}}
            </nuxt-link>
          </template>
        </template>
      </div>

      <div id="nav" class="navbar-menu">
        <div class="navbar-end">
         <template v-if="!$auth.user"> 
            <nuxt-link :to="{name: 'auth-login'}" class="navbar-item">Sign in</nuxt-link>
          </template>
          <template v-else>
            <a class="navbar-item" href="">{{$auth.user.name}}</a>
            <a class="navbar-item" href="">Orders</a>
            <a class="navbar-item" href="">Cart (0)</a>
          </template>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters({
      categories: "categories"
    })
  }
};
</script>
