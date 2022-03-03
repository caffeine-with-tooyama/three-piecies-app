<template>
  <h1>Home</h1>
  <nav class="navigation">
    <router-link
      to="/"
      class="itojun__link"
      exact-active-class="navigation__link--exact-active"
      >Home</router-link
    >

    <router-link
      to="/quiz"
      class="itojun__link"
      exact-active-class="navigation__link--exact-active"
      >Vue クイズ</router-link
    >
    <router-link
      to="/palette"
      class="itojun__link"
      exact-active-class="navigation__link--exact-active"
      >Vue パレット</router-link
    >
    <router-link
      to="/memo"
      class="itojun__link"
      exact-active-class="navigation__link--exact-active"
      >Vue メモ</router-link
    >
  </nav>
  <div class="shindan" id="app">
    <div class="probably">ローマ字で名前を書いてね！</div>
    <div class="searchform">
      <input type="text" v-model="namevalue" size="20*20" />
    </div>

    <div class="button">
      <button v-on:click="searchName">性別判定</button>
    </div>

    <div class="search">
      <span class="probably">{{ probably }}</span
      >{{ onamae }}{{ sex }}
    </div>
    <div
      class="taka"
      v-bind:style="{ backgroundImage: 'url(' + takachan + ')' }"
    ></div>
  </div>
</template>

<script>
import AssetsTakachan from "@/assets/20220227_153138.jpg"
export default {
  name: "app",
  data() {
    return {
      sex: "",
      namevalue: "",
      onamae: "",
      takachan: "",
      probably: "",
    }
  },
  methods: {
    searchName: async function () {
      this.onamae = this.namevalue
      const res = await fetch(`https://api.genderize.io/?name=${this.onamae}`)
      const value = await res.json()
      this.probably = await value.probability
      this.probably = this.probably * 100 + "%"
      if (this.namevalue == "takahiro") {
        this.sex = "は男です"
        this.takachan = AssetsTakachan
      } else if ((await value.gender) == "male") {
        this.sex = "は男です"
      } else if ((await value.gender) == "female") {
        this.sex = "は女です"
      }
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  color: rgb(53, 46, 35);
}
.itojun__link {
  background-color: rgb(228, 228, 228);
  width: 10rem;
  height: 10rem;
  color: rgb(53, 46, 35);
  text-align: center;
  font-size: 1.5rem;
  transition: color 0.3s;
  border-radius: 1rem;
}
nav {
  display: flex;
  width: 80%;
  height: 10rem;
  margin-left: 10%;
  justify-content: space-between;
}
.taka {
  width: 60%;
  height: 60rem;
  background-size: cover;
  margin: 0 auto;
}
.search {
  width: 100%;

  font-size: 5rem;
}
.shindan {
  text-align: center;
}
.probably {
  color: rgb(53, 46, 35);
  font-size: 5rem;
}
a {
  color: aliceblue;
}
</style>
