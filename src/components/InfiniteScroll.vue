<script setup>
import { ref } from "vue";
import getUsers from "../api/getUsers.js";
import { useInfiniteScroll } from "@vueuse/core";
import axios from "axios";

const listElement = ref(null);
const usersToShow = 15;

const usersList = ref(await getUsers(usersToShow, 0));

const fetchingData = ref(null);

const getUsersOnScroll = async () => {
  fetchingData.value = true;
  await new Promise((res) => setTimeout(res, 2000));

  try {
    const newUsers = await getUsers(usersToShow, usersList.value.length);

    fetchingData.value = null;
    usersList.value.push(...newUsers);
  } catch (error) {
    console.log(error);
  }
};

useInfiniteScroll(
  listElement,
  async () => {
    await getUsersOnScroll();
  },
  { distance: 10 }
);
</script>

<template>
  <section>
    <ul ref="listElement">
      <li v-for="user in usersList" :key="user.id">
        {{ user.firstName }}
      </li>

      <p v-show="fetchingData" class="loading-msg">
        Fetching more users... Please hold
      </p>
    </ul>
  </section>
</template>

<style scoped>
section {
  display: flex;
  align-items: center;
  justify-content: center;
}

ul {
  background-color: #173d2c;
  list-style: none;
  max-height: 600px;
  width: 600px;
  overflow-y: scroll;
  padding: 12px 20px;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  text-align: left;
}

li {
  padding: 12px 0;
  color: #fff;
  font-size: 18px;
}

.loading-msg {
  color: goldenrod;
  font-size: 20px;
}
</style>