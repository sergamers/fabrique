<template>
  <div>
    <div>Тип карты лояльности <br /><br /></div>

    <div v-for="(type, index) in types" :key="type.idEl">
      <select v-model="type.data.type">
        <option :value="null"></option>
        <option value="gold">Gold</option>
        <option value="silver">Silver</option>
        <option value="black">Black</option>
      </select>

      <button v-if="types.length > 1" @click="deleteType(index)">
        Удалить тип
      </button>
    </div>

    <br /><br />

    <button @click="addType()">Добавить тип</button>
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
