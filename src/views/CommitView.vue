<template>
  <div class="commit">
    <div class="maincont container drop-shadow">
      <div class="maincont container-sm col-md-4">
        <button class="btn" type="button" @click="$router.push('/')">
          <img src="https://cdn-icons-png.flaticon.com/512/467/467274.png" />
        </button>
        <div class="subcont container-md">
          <table class="table">
            <thead>
              <tr>
                <th class="table-col">Name</th>
                <th>{{ currentName }}</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="table-col">Email</td>
                <td>{{ currentEmail }}</td>
              </tr>
              <tr>
                <td class="table-col">Message</td>
                <td>{{ currentMessage }}</td>
              </tr>
              <tr>
                <td class="table-col">Date</td>
                <td>{{ currentDate }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "CommitPage",
  props: ["sha"],
  data: function () {
    return {
      ime: "commit",
      currentName: [],
      currentEmail: [],
      currentMessage: [],
      currentDate: [],
    };
  },
  async mounted() {
    let commitsResponse = await fetch(
      "https://api.github.com/repos/vuejs/vue/commits"
    );
    let commits = await commitsResponse.json();

    let pathName = window.location.pathname.split("/");
    let currentSha = pathName[2];

    for (let item of commits) {
      if (item.sha == currentSha) {
        this.currentName = item.commit.author.name;
        this.currentEmail = item.commit.author.email;
        this.currentMessage = item.commit.message;
        this.currentDate = item.commit.author.date;
      }
    }
  },
};
</script>

<style>
.btn {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  display: flex;
  justify-content: start;
  margin-left: -20px;
  margin-top: -10px;
  background-color: #dcdde2;
  border: 2px solid black;
  transition-duration: 0.4s;
}
.btn:hover {
  background-color: lightblue;
}
button > img {
  vertical-align: middle;
}
img {
  height: 36px;
  width: auto;
  margin-top: 7px;
}
th,
td {
  font-weight: normal;
  border-bottom: 0.5px solid black;
  padding: 17px 40px 7px 40px;
}
tr:hover {
  background-color: aliceblue;
}
table {
  margin: auto;
  margin-top: 30px;
  border-bottom: 0.5px solid black;
  border-collapse: collapse;
  border-spacing: 20px 20px;
}
.table-col {
  background-color: #c8dbdf;
  border-right: 0.5px solid black;
}
.subcont {
  overflow-x: auto;
}
.subcont::-webkit-scrollbar {
  height: 12.2px;
  background-color: lightgrey;
  border-radius: 100px;
}
.subcont::-webkit-scrollbar-thumb {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.7);
  border-radius: 100px;
  border: 0.2px solid rgba(0, 0, 0, 0.2);
}
</style>
