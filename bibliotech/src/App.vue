<template>
  <div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "app",
  created() {
    document.title = "Bibliotech";
  },
};
</script>
