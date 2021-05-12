<template >
  <div>
      <Sidebar :client="client" />
  </div>
</template>


<script>
import Sidebar from "./components/Sidebar.vue";

export default {
  mounted() {
    this.get();
  },
  name: "App",
  components: {
    Sidebar,
  },
  data() {
    return {
      client: {}
    };
  },
  methods: {
    get() {
      app.initialized().then((client) => {
        this.client = client;
      });
    },
  },
};

</script>

<style scoped>
</style>


