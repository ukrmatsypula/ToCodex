<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <table>
          <thead>
            <tr>
              <th @click="sort('name')">Name &#8609;</th>
              <th @click="sort('age')">Age &#8609;</th>
              <th @click="sort('gender')">Gender &#8609;</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="user in usersSort" :key="user.id">
              <td>
                <img :src="user.img" :alt="user.name" />
                <span>{{ user.name }}</span>
              </td>
              <td>{{ user.age }}</td>
              <td>{{ user.gender }}</td>
            </tr>
          </tbody>
        </table>
        <p>
          debug: sort: {{ this.currentSort }}, dir: {{ this.currentSortDir }}
        </p>
      </div>
    </section>

    <!-- buttons -->
    <section>
      <div class="contaier">
        <div class="button-list">
          <div class="btn btnPrimary">&#8592;</div>
          <div class="btn btnPrimary">&#8594;</div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    users: [],
    currentSort: "name",
    currentSortDir: "asc",
  }),
  computed: {
    usersSort() {
      return this.users.sort((a, b) => {
        let mod = 1;
        if (this.currentSortDir === "desc") {
          return (mod = -1);
        }
        if (a[this.currentSort] < b[this.currentSort]) {
          return -1 * mod;
        }
        if (a[this.currentSort] > b[this.currentSort]) {
          return 1 * mod;
        }
        return 0;
      });
    },
  },
  methods: {
    sort(e) {
      if (e === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = e;
    },
  },
  created() {
    axios
      .get("http://localhost:3000/users")
      .then((response) => (this.users = response.data))
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-right: 16px;
}
.button-list {
  width: 100%;
  text-align: center;

  .btn {
    border-radius: 60px;
    margin: 0 20px;
  }
}
</style>
