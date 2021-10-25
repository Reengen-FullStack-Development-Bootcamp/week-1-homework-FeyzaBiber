<template>
  <div id="app">
    <Header />

    <!---------->
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="#">Shopping Card</b-navbar-brand>

      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown
          right
          size="lg"
          variant="link"
          toggle-class="text-decoration-none"
          no-caret
          class="my-2 my-sm-0"
        >
          <template #button-content>
            &#128722;
            <b-badge variant="light">{{ basketAllItemCount }}</b-badge>
          </template>
          <b-dropdown-item v-show="this.basket.length === 0">
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
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-navbar>
    <!---------->
    <b-container>
      <b-col class="CardBox d-flex flex-row justify-content-around">
        <product-card
          class="CardBox"
          v-for="(item, i) in productInfoList"
          :key="i"
          :info="item"
          @addProduct="
            productCal({ value: $event, type: 'add' });
            showDismissibleAlert = true;
          "
        />
      </b-col>
    </b-container>
  </div>
</template>


<script>
import Header from "./components/Header.vue";
import ProductCard from "./components/ProductCard";

export default {
  name: "App",
  components: {
    ProductCard,
    Header,
  },
  data() {
    return {
      title: "Shopping Card",
      showDismissibleAlert: false,
      productInfoList: [
        {
          image: "nike-pink.jpg",
          title: "1 Nike Epic React Flyknit Pearl Pink",
          color: "pink",
          description:
            "This attraction of opposites creates a sensation that not only enhances the feeling of moving forwards, but makes running feel fun, too.",
          rating: 1,
          shortName: "Nike Pearl Pink",
          price: 150,
          Amount: 0,
          selectedSize: 0,
        },
        {
          image: "nike-blue.jpg",
          title: "2 Nike Epic React Flyknit Blue",
          color: "blue",
          description:
            "This attraction of opposites creates a sensation that not only enhances the feeling of moving forwards, but makes running feel fun, too.",
          rating: 2,
          shortName: "Nike Blue",
          price: 150,
          Amount: 0,
          selectedSize: 0,
        },
        {
          image: "nike-pink.jpg",
          title: "3 Nike Epic React Flyknit Pearl Pink",
          color: "pink",
          description:
            "This attraction of opposites creates a sensation that not only enhances the feeling of moving forwards, but makes running feel fun, too.",
          rating: 3,
          shortName: "Nike Pearl Pink",
          price: 150,
          Amount: 0,
          selectedSize: 0,
        },
        {
          image: "nike-blue.jpg",
          title: "4 Nike Epic React Flyknit Blue",
          color: "blue",
          description:
            "This attraction of opposites creates a sensation that not only enhances the feeling of moving forwards, but makes running feel fun, too.",
          rating: 4,
          shortName: "Nike Blue",
          price: 150,
          Amount: 0,
          selectedSize: 0,
        },
      ],
      basket: [],
    };
  },
  computed: {
    basketAllItemCount() {
      let count = 0;
      for (let i = 0; i < this.basket.length; i++) {
        count += this.basket[i].count;
      }
      return count;
    },
  },
  methods: {
    productCal(val) {
      let index = this.basket.findIndex((el) => el.title === val.value.title);
      switch (val.type) {
        case "add":
          if (index >= 0) {
            this.basket[index].count++;
          } else {
            this.basket.unshift({ ...val.value, count: 1 });
          }
          break;
        case "+":
          this.basket[index].count++;
          break;
        case "-":
          if (this.basket[index].count > 1) {
            this.basket[index].count--;
          } else {
            this.basket.splice(index, 1);
          }
          break;
        case "del":
          this.basket.splice(index, 1);
          break;
        default:
      }
    },
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #c8dbee;
  margin-top: 0px;

  display: flex;
  flex-flow: column;
  height: 100%;
}

.CardBox {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-bottom: 10px;
  margin-top: 10px;
}
</style>





