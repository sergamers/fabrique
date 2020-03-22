<template>
  <div class="ExtraCondition">

    <div class="ExtraCondition-content">
      <div class="ExtraCondition-range" v-for="(type, index) in types" :key="type.idEl">
        <div class="ExtraCondition-titleWrapper">
          <div class="ExtraCondition-or" v-if="(index >= 1)">ИЛИ</div>
          <div class="ExtraCondition-title">Тип {{index + 1}}</div>

        </div>

        <select class="ExtraCondition-select" v-model="type.data.type">
          <option :value="null"></option>
          <option value="gold">Gold</option>
          <option value="silver">Silver</option>
          <option value="black">Black</option>
        </select>

        <button class="ExtraCondition-button ExtraCondition-button--red ExtraCondition-delete" v-if="types.length > 1" @click="deleteType(index)">
          X
        </button>
      </div>
    </div>

    <button class="ExtraCondition-button ExtraCondition-button--green ExtraCondition-add" @click="addType()">+ Добавить тип</button>
  </div>
</template>

<script>
export default {
  name: "TypeCondition",
  data: () => ({
    idEl: 0,
    types: []
  }),
  created: function() {
    this.addType();
    this.$emit("createForm", this.types);
  },
  methods: {
    addType: function() {
      this.types.push({
        idEl: ++this.idEl,
        data: {
          type: null
        }
      });
    },
    deleteType: function(index) {
      this.types.splice(index, 1);
    }
  }
};
</script>

<style lang="scss" src="@/styles/components/ages-condition.scss"></style>
