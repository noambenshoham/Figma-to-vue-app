<script setup>
import ContractCard from "./components/ContractCard.vue";
import axios from "axios";
import { ref } from "vue";

const projects = ref({});
axios
  .get(`https://63d23c0906556a0fdd376b3c.mockapi.io/projects`)
  .then((res) => {
    projects.value = res.data;
  });
</script>

<template>
  <div class="App">
    <div class="app-container">
      <div class="header">Contracts</div>
      <div class="main">
        <div class="search-bar-container">
          <input
            class="search-bar"
            type="search"
            placeholder="Search Customer"
            v-model="input"
          />
          <img src="{SearchIcon}" />
        </div>
        <div class="contracts-container">
          <div v-for="project in projects">
            <ContractCard :project="project" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
* {
  font-family: "Poppins";
  font-style: normal;
}

body {
  font-family: "Poppins";
  font-style: normal;
  background: #f6f9fa;
}

.App {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .header {
    font-family: "Poppins";
    font-style: normal;
    font-weight: 600;
    font-size: 32px;
    line-height: 48px;
    letter-spacing: 0.436364px;
    color: #2d2d2d;
  }

  .main {
    padding: 10px;
    background: #ffffff;
    border: 1px solid #ddedf4;
    border-radius: 9px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    gap: 20px;

    .contracts-container {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      gap: 16px;
    }
    @media (min-width: 768px) {
      .contracts-container {
        flex-flow: row wrap;
        justify-content: flex-start;
        flex-direction: unset;
        width: 720px;
      }
    }
    @media (min-width: 1130px) {
      .contracts-container {
        width: 1088px;
      }
    }
  }
}
@media (min-width: 768px) {
  .header {
    align-self: flex-start;
  }
  .contracts-container {
    flex-flow: row wrap;
    justify-content: flex-start;
    flex-direction: unset;
    width: 720px;
  }
  .search-bar-container {
    width: auto;
    height: 46px;
    position: relative;

    .search-bar {
      border-radius: 7px;
      border: 2px #2d2d2d solid;
      opacity: 0.5;
      text-indent: 10px;

      width: 100%;
      height: 100%;
    }
    img {
      position: absolute;
      right: 14.33px;
      top: 15px;
    }
  }

  @media (min-width: 768px) {
    .search-bar-container {
      width: 289px;
    }
  }
}
</style>
