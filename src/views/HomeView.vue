<template>
  <div class="home">
    <div class="maincont maincont-scroll-hidden container drop-shadow">
      <div class="maincont maincont-scroll container-sm col-md-4">
        <ul>
          <li v-for="item in commits" v-bind:key="item.sha">
            Commit
            <router-link :to="'/commit/' + item.sha" class="routerlink">{{
              item.sha
            }}</router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data: function () {
    return {
      ime: "home",
      commits: [],
    };
  },
  async mounted() {
    let rezultat = await fetch(
      "https://api.github.com/repos/vuejs/vue/commits"
    );

    let podaci = await rezultat.json();

    for (let item of podaci) {
      console.log(item.sha);
    }
    this.commits = podaci;
  },
};
</script>

<style>
html {
  background-color: #b7ced2;
}
.maincont {
  display: inline-block;
  border: 1px solid #dcdde2;
  background-color: #dcdde2;
  text-align: center;
  width: 50rem;
  max-width: 80%;
  padding: 40px;
}
.maincont {
  overflow-x: auto;
}
.maincont-scroll-hidden {
  overflow-x: hidden;
}
.maincont-scroll::-webkit-scrollbar {
  height: 12.2px;
  background-color: lightgrey;
  border-radius: 100px;
}
.maincont-scroll::-webkit-scrollbar-thumb {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.7);
  border-radius: 100px;
  border: 0.2px solid rgba(0, 0, 0, 0.2);
}
.drop-shadow {
  margin: 0;
  padding: 0;
  -webkit-box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.5);
  box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.5);
}
ul {
  list-style-type: circle;
  display: inline-block;
}
li {
  color: #191e21;
  text-align: center;
  font-size: 14.3px;
  margin: 5px;
  padding: 3px;
}
.routerlink {
  color: #528e86;
}
</style>
