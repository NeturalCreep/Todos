<template>
  <div class="home">
    <Todo msg="普通" content="Normal" />
    <Todo msg="重要" content="Imporant" />
    <Todo msg="公司" content="Corp" />
    <Todo msg="家庭" content="Family" />
  </div>
</template>

<style>
.home {
  height: 100%;
  flex-flow: row wrap;
  align-content: flex-start;
  display: flex;
}
</style>

<script>
// @ is an alias to /src
import Todo from "@/components/Todo.vue";

export default {
  name: "home",
  method: {},
  components: {
    Todo
  }
};
</script>
