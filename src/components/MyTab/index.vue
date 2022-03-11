<template>
  <div>
    <table border="1" width="300px">
      <thead>
        <th @click="sortByName">Name</th>
        <th @click="sortByPower">Power</th>
      </thead>
      <tbody>
        <tr v-for="item in newMember" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.power }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
function sortRulePowerAsc(a, b) {
  if (a.power === "infinity")   return '999999' - b.power;;
  if (b.power === "infinity") return a.power - '9999999';
  return a.power - b.power;
}

function sortRulePowerDesc(a, b) {
  if (a.power === "infinity")   return b.power - '999999999';
  if (b.power === "infinity")   return '999999999' - a.power;
  return b.power - a.power;
}

function sortRuleNameAsc(a, b) {
  return a.name > b.name ? 1 : -1;
}

function sortRuleNameDesc(a, b) {
  return a.name > b.name ? -1 : 1;
}

export default {
  name: "MyTab",
  data() {
    return {
      member: [
        {
          id: 1,
          name: "Jackie Chan",
          power: "10000",
        },
        {
          id: 2,
          name: "Jet Li",
          power: "8000",
        },
        {
          id: 5,
          name: "Bruce Lee",
          power: "9000",
        },
        {
          id: 4,
          name: "Chuck Norris",
          power: "infinity",
        },
      ],
      searchWhat: "",
      flagPower: true,
      flagName: true,
    };
  },
  mounted() {
    let _this = this;
    this.$bus.$on("searchUser", function (item) {
      _this.searchWhat = item;
    });
  },
  methods: {
    sortByName() {
      if (this.flagName) {
        this.member.sort(sortRuleNameAsc);
        this.flagName = false;
      } else {
        this.member.sort(sortRuleNameDesc);
        this.flagName = true;
      }
    },
    sortByPower() {
      if (this.flagPower) {
        this.member.sort(sortRulePowerAsc);
        this.flagPower = false;
      } else {
        this.member.sort(sortRulePowerDesc);
        this.flagPower = true;
      }
    },
  },
  computed: {
    newMember() {
      let _this = this;
      if (!this.searchWhat) {
        return this.member;
      } else {
        return this.member.filter(
          (item) =>
            item.power.indexOf(_this.searchWhat) !== -1 ||
            item.name.toLowerCase().indexOf(_this.searchWhat.toLowerCase()) !== -1
        );
      }
    },
  },
};
</script>

<style>
</style>