<template>
  <div class="header">
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Shopping Card</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"> </b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-dropdown
            size="lg"
            variant="link"
            toggle-class="text-decoration-none"
            no-caret
            right
            class="my-2 my-sm-0"
          >
            <template #button-content>
              &#128722;
              <b-badge variant="light">{{ basketAllItemCount }}</b-badge>
            </template>
            <b-dropdown-item v-show="basket.length === 0">
              Product Cart is empty
            </b-dropdown-item>
            <b-dropdown-item v-for="(el, i) in basket" :key="i">
              {{ el.title }} - {{ (el.price * el.count).toFixed(2) }}$
              <b-button
                class="mx-2"
                @click="productCal({ value: el, type: '-' })"
                variant="dark"
                size="sm"
                >-</b-button
              >
              <b-button
                class="mx-2"
                @click="productCal({ value: el, type: '+' })"
                variant="success"
                size="sm"
                >+</b-button
              >
              <b-button
                @click="productCal({ value: el, type: 'del' })"
                variant="danger"
                size="sm"
                >X</b-button
              >
            </b-dropdown-item>
          </b-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>

nav{
  background-color: #f6f4f5;
  width: auto;
  height: 50px;
  box-shadow: 1px 1px 3px rgba(112, 128, 144, 0.61);
  
}

</style>
