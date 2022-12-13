<template>
  <div>
    {{ count }}
    <span>{{ count }}</span>
    <Button foo="hello!"><span>slot</span></Button>
  </div>
</template>

<script>
import Button from "./Button.vue";

export default {
  data() {
    return {
      count: 0,
      color: "blue",
    };
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
.logo {
  width: 100px;
  border: 1px solid v-bind(color);
}
</style>
