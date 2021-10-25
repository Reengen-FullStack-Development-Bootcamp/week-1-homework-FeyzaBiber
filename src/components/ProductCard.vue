<template>
  <div>
    <div class="alert-box">
      <b-alert v-model="showDismissibleAlert" variant="success" dismissible>
        The Product has been added 👍🏻
      </b-alert>
    </div>

    <div>
      <b-card no-body class="overflow-hidden" style="max-width: 450px">
        <b-row no-gutters>
          <b-col md="6">
            <b-card-img
              :src="require('../assets/' + info.image)"
              :alt="info.shortName"
              class="rounded-0 imgcss"
            ></b-card-img>

            <v-rating
              :value="4.5"
              color="amber"
              dense
              half-increments
              readonly
              size="14"
            ></v-rating>

            <div>
              <span
                v-for="(el, i) in info.rating"
                :key="i"
                class="fa fa-star checked"
              />
              <span
                v-for="(el, i) in 5 - info.rating"
                :key="'empty-' + i"
                class="fa fa-star"
              />
            </div>

            <div :class="info.color" class=""></div>
          </b-col>
          <b-col md="6">
            <b-card-body :class="info.color" :title="info.title" class="title">
              <b-card-text :class="info.color" class="body">
                {{ info.description }}
              </b-card-text>
            </b-card-body>
          </b-col>
        </b-row>
        <b-row>
          <div :class="this.color" class="sizebutton">
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(5)"
              :class="info.color"
            >
              5
            </b-button>
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(6)"
              :class="info.color"
            >
              6
            </b-button>
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(7)"
              :class="info.color"
            >
              7
            </b-button>
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(8)"
              :class="info.color"
            >
              8
            </b-button>
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(9)"
              :class="info.color"
            >
              9
            </b-button>
            <b-button
              variant="outline-secondary"
              class="sizebutton"
              @click="changeSize(10)"
              :class="info.color"
            >
              10
            </b-button>

            <select
              :class="info.color"
              name="value"
              id="value"
              class="Amountselect"
              v-model="Amount"
            >
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
              <option value="5">5</option>
              <option value="6">6</option>
              <option value="7">7</option>
              <option value="8">8</option>
              <option value="9">9</option>
              <option value="10">10</option>
            </select>

            <h4 :class="info.color">
              <b-badge type="dark" variant="light" :class="info.color"
                >{{ Cost }} $</b-badge
              >
            </h4>
            <b-button
              pill
              variant="outline-secondary"
              :class="info.color"
              @click="addToBasket(info)"
            >
              Buy
            </b-button>
          </div>
        </b-row>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    info: Object,
  },
  data() {
    return {
      Amount: 1,
      selectedSize: 5,
    };
  },
  methods: {
    addToBasket(val) {
      this.$emit("addProduct", val);
     
    },
    changeSize(val) {
      this.selectedSize = val;
    },
    changeAmount(val) {
      this.Amount = val;
    },
  },

  computed: {
    Cost() {
      let cost = Math.floor(
        (this.info.price + this.selectedSize) * this.Amount
      );
      return cost;
    },
  },
};
</script>

<style scoped>
.checked {
  color: orange;
}

.pink {
  color: rgb(195, 161, 160);
}

.blue {
  color: rgb(124, 205, 230);
}

.body {
  font-size: 12px;
  text-align: left;
  color: gray;
}
.title {
  font-size: 16px;
  text-align: left;
}

.sizebutton {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 50px;
  height: 35px;
  margin: 4px 2px;
}

.sizebutton {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 60px;
  height: 35px;
  margin: 4px 2px;
}

.pink-border {
  border-color: rgb(195, 161, 160);
}
.blue-border {
  border-color: rgb(124, 205, 230);
}
.imgcss {
  display: flex;
  justify-content: space-between;
  margin: 4px 2px;
}
.Amountselect {
  width: 50px;
  height: 35px;
  margin: 4px 2px;
  border-color: gray;
}
</style>
