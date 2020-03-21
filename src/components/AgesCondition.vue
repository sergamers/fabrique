<template>
  <div>
    <div>Возраст респондента <br /><br /></div>

    <div v-for="(range, index) in ranges" :key="range.idEl">
      <div>
        от <input type="text" v-model="range.data.from" /> до
        <input type="text" v-model="range.data.to" />

        <button v-if="ranges.length > 1" @click="deleteRange(index)">
          Удалить диапазон
        </button>
      </div>
    </div>

    <br /><br />

    <button @click="addRange()">Добавить диапазон</button>
  </div>
</template>

<script>
export default {
  name: "AgesCondition",
  data: () => ({
    ranges: [],
    idEl: 0
  }),
  created: function() {
    this.addRange();
    this.$emit("createForm", this.ranges);
  },
  methods: {
    addRange: function() {
      this.ranges.push({
        idEl: ++this.idEl,
        data: {
          from: null,
          to: null
        }
      });
    },
    deleteRange: function(index) {
      this.ranges.splice(index, 1);
    }
  }
};
</script>
