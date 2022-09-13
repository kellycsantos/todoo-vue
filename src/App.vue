<template>
  <div class="container" :style="theme">
    <span class="select-theme">
      Escolha um tema :
      <select v-model="color">
        <option v-for="(theme, index) in themes" :key="index" :value="theme">
          {{ theme.title }}
        </option>
      </select>
    </span>

    <TodoView />
  </div>
</template>

<script>
import TodoView from "./components/TodoView.vue";

export default {
  components: {
    TodoView,
  },
  data() {
    return {
      color: null,
      themes: [
        { title: "Hello Jadoo", imgName: "jadoo", color: "#B6E2A3" },
        { title: "My Melody", imgName: "melo-piano-kuromi", color: "#fed4de" },
        { title: "Tonari no Totoro", imgName: "totoro", color: "#EEEAE7" },
        { title: "Nagatoro", imgName: "nagatoro", color: "#FFFFFF" },
      ],
      theme: {
        background: `url(${require(`./assets/background/jadoo.jpg`)}) no-repeat center `,
      },
    };
  },
  methods: {},
  mounted() {
    this.theme.background = ` ${
      this.themes[0].color
    } url(${require(`./assets/background/${this.themes[0].imgName}.jpg`)}) no-repeat center `;
  },
  watch: {
    color(val) {
      this.theme.background = ` ${
        val.color
      } url(${require(`./assets/background/${val.imgName}.jpg`)}) no-repeat center `;
      this.color = val;
    },
  },
};
</script>

<style>
* {
  margin: 0;
}
.container {
  width: 100vw;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}
.select-theme {
  align-self: flex-start;
  margin: 15px 0 5px 5px;
}
#app {
  font-family: "Montserrat", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
