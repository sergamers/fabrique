<template>
  <div class="ExtraCondition">
    <div class="ExtraCondition-content">
      <div class="ExtraCondition-range" v-for="(range, index) in ranges" :key="range.idEl">
        <div class="ExtraCondition-titleWrapper">
          <div class="ExtraCondition-or" v-if="(index >= 1)">ИЛИ</div>
          <div class="ExtraCondition-title">Диапазон {{index + 1}}</div>
        </div>

        от <input class="ExtraCondition-input ExtraCondition-input--small" type="text" v-model="range.data.from" /> до
        <input class="ExtraCondition-input ExtraCondition-input--small" type="text" v-model="range.data.to" />

        <button class="ExtraCondition-button ExtraCondition-button--red ExtraCondition-delete" v-if="ranges.length > 1" @click="deleteRange(index)">
          X
        </button>
      </div>
    </div>

    <button class="ExtraCondition-button ExtraCondition-button--green ExtraCondition-add" @click="addRange()">+ Добавить диапазон</button>
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

<style lang="scss" src="@/styles/components/ages-condition.scss"></style>
