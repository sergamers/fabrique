<template>
  <div>
    <div>Статус карты лояльности <br /><br /></div>

    <div v-for="(status, index) in statuses" :key="status.idEl">
      <select v-model="status.data.status">
        <option :value="null"></option>
        <option value="active">Активна</option>
        <option value="disabled">Заблокированна</option>
        <option value="inProcess">В обработке</option>
      </select>

      <button v-if="statuses.length > 1" @click="deleteStatus(index)">
        Удалить статус
      </button>
    </div>

    <br /><br />

    <button @click="addStatus()">Добавить статус</button>
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
