<template>
  <div class="table">
    <div class="row" v-for="row in table" :key="row.id">
      <input
        :class="{ pointer: readonly }"
        type="text"
        placeholder="Категория"
        v-model="row.header"
        class="row-header"
        :readonly="readonly"
        :ref="'tableCategory' + row.id"
        @keypress.enter="$emit('enterPress', row.id)"
      />
      <span
        class="column"
        v-for="(column, index) in row.cols"
        :key="index"
        @click="$emit('tableClick', [row.id, index])"
        >{{ column.score }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    table: {
      type: Array,
      require: true,
    },
    readonly: {
      type: Boolean,
      default: true,
    },
  },
};
</script>

<style scoped>
input,
span {
  resize: none;
  text-align: center;
  background-color: initial;
}
.pointer {
  cursor: pointer;
}
.table {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 100%;
  height: 100%;
}
.header {
  font-size: 30px;
}
.row {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 100%;
}
.row-header {
  max-width: 200px;
  text-align: center;
  color: var(--color-font-main);
  font-size: 40px;
}

.column {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: 0.2s;
  font-size: 50px;
  border-radius: 10px;
  width: 10%;
  height: 70%;
}

.column:hover {
  background-color: rgba(0, 0, 0, 0.404);
}
@media (max-width: 1200px) {
  .column {
    font-size: 30px;
  }
  .row-header{
    font-size: 25px;
  }
}
</style>
