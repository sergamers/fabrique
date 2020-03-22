<template>
  <div class="ExtraCondition">

    <div class="ExtraCondition-content">
      <div class="ExtraCondition-range" v-for="(status, index) in statuses" :key="status.idEl">
        <div class="ExtraCondition-titleWrapper">
          <div class="ExtraCondition-or" v-if="(index >= 1)">ИЛИ</div>
          <div class="ExtraCondition-title">Статус {{index + 1}}</div>
        </div>

        <select class="ExtraCondition-select" v-model="status.data.status">
          <option :value="null"></option>
          <option value="active">Активна</option>
          <option value="disabled">Заблокированна</option>
          <option value="inProcess">В обработке</option>
        </select>

        <button class="ExtraCondition-button ExtraCondition-button--red ExtraCondition-delete" v-if="statuses.length > 1" @click="deleteStatus(index)">
          X
        </button>
      </div>
    </div>

    <button class="ExtraCondition-button ExtraCondition-button--green ExtraCondition-add" @click="addStatus()">+ Добавить статус</button>
  </div>
</template>

<script>
export default {
  name: "StatusCondition",
  data: () => ({
    idEl: 0,
    statuses: []
  }),
  created: function() {
    this.addStatus();
    this.$emit("createForm", this.statuses);
  },
  methods: {
    addStatus: function() {
      this.statuses.push({
        idEl: ++this.idEl,
        data: {
          status: null
        }
      });
    },
    deleteStatus: function(index) {
      this.statuses.splice(index, 1);
    }
  }
};
</script>

<style lang="scss" src="@/styles/components/ages-condition.scss"></style>
