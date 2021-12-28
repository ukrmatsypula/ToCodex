<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Age</th>
              <th>Gender</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="user in users" :key="user.id">
              <td>{{ user.name }}</td>
              <td>{{ user.age }}</td>
              <td>{{ user.gender }}</td>
            </tr>
          </tbody>
        </table>
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
  }),
  created() {
    this.users = [
      { id: 1, name: "Jack", age: 22, gender: "male" },
      { id: 2, name: "Alex", age: 24, gender: "male" },
    ];
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 60px;
  height: auto;
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
