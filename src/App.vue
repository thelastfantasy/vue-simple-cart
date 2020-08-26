<template>
  <div id="app">
    <h2>{{ time }}</h2>
    <div v-if="items.length">
      <table>
        <thead>
          <tr>
            <th v-show="showId"></th>
            <th>商品</th>
            <th>値段</th>
            <th>数</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <td v-show="showId">{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.price | toCurrency }}</td>
            <td>
              <button @click="decrement(item)" :disabled="item.count <= 1">-</button>
              <span class="w-40 center">{{ item.count }}</span>
              <button @click="increment(item)">+</button>
            </td>
            <td>
              <button @click="removeHandler(index)">削除</button>
            </td>
          </tr>
        </tbody>
      </table>
      合計：{{ totalPrice | toCurrency }}
    </div>
    <h2 id="card-empty" v-else>カートになんにもないです</h2>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      showId: 1,
      time: new Date(),

      items: [
        {
          id: 1,
          name: "スーパードライ 350ml",
          count: 1,
          price: 200.5,
        },
        {
          id: 2,
          name: "金麦 350ml",
          count: 1,
          price: 210,
        },
        {
          id: 3,
          name: "モルツ 350ml",
          count: 1,
          price: 220,
        },
        {
          id: 4,
          name: "華みやび 350ml",
          count: 1,
          price: 350,
        },
      ],
    };
  },

  computed: {
    totalPrice() {
      let total = 0;
      for (const item of this.items) {
        total += item.price * item.count;
      }
      return total;
    },
  },

  methods: {
    decrement(item) {
      item.count--;
    },

    increment(item) {
      item.count++;
    },

    removeHandler(index) {
      this.items.splice(index, 1);
    },
  },

  filters: {
    toCurrency(price) {
      return "￥" + price.toFixed(2);
    },
  },

  mounted() {
    setInterval(() => {
      this.time = new Date();
    }, 500);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#card-empty {
  color: #f00;
}

@import "./assets/styles/style.css";
</style>
