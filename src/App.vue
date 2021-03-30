<template >
  <div>
    <div v-if="location === 'ticket_sidebar'">
      <Sidebar :agentName="name" />
    </div>
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
      location: "",
      name: "",
    };
  },
  methods: {
    get() {
      app.initialized().then((client) => {
        client.data.get("contact").then(
          (data) => {
            this.name = data.contact.name;
          },
          (error) => {
            console.error("error", error);
          }
        );
        this.interface(client);
      });
    },
    interface(client) {
      client.instance.context().then((context) => {
        this.location = context.location;
      });
    },
    instance() {
      
    },
  },
};
// app.initialized().then((client) => {
//   console.log("client", client);
//   client.data.get("contact").then(
//     (data) => {
//       console.log("data", data.contact.name);
//     },
//     (error) => {
//       console.error("error", error);
//     }

//   );
// });
</script>

<style scoped>
</style>


