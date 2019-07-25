<template>
  <div>
    <div v-bind:key="agent.id" v-for="agent in agents">
      <Agent v-bind:agent="agent" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Agent",
  props: ["agent"]
};
</script>

<style scoped>
.agent {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>

