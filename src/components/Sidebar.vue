<template>
  <div id="app" class="App">
    <h3>Fetch Current Location of International Space Station</h3>
    <fw-button id="fetch" v-on:click="fetchData()" color="secondary">
      Fetch and Save
    </fw-button>
    <h3>Fetch the saved location from DB</h3>
    <fw-button id="fetch" v-on:click="fetchFromDataStorage()" color="secondary">
      Fetch
    </fw-button>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  props: {
    client: Object,
  },
  data() {
    return {
      ticketID: "",
    };
  },
  methods: {
    fetchData() {
      // API endpoint to fetch the current location of the International Space Station
      const API_BASE_URL =
        "https://api.wheretheiss.at/v1/satellites/25544/positions";

      // Timestamp for current time to get the location of International Space Station for a specified time.
      const timestamp = new Date().getTime();

      // HTTP request header
      const headers = {
        "Content-Type": "application/json",
      };

      // Options passed to the request method, consists of header, body and other objects with multiple functionalities
      const options = {
        headers,
      };

      // HTTP request to get the date from the
      this.client.request
        .get(`${API_BASE_URL}?timestamps=${timestamp}&units=miles`, options)
        .then(
          (location) => {
            this.saveInDataStorage({
              latitude: JSON.parse(location.response)[0].latitude,
              longitude: JSON.parse(location.response)[0].longitude,
            });
          },
          (error) => {
            // Error handling
            console.error("error", error);
          }
        );
    },
    saveInDataStorage(location) {
      this.client.db.set("location", location).then(
        (data) => {
          this.showNotify(
            "success",
            "Location saved successfully in the Data Storage"
          );
          console.info(data);
        },
        (error) => {
          console.error(error);
        }
      );
    },
    fetchFromDataStorage() {
      this.client.db.get("location").then(
        (data) => {
          this.showNotify(
            "success",
            `The location of ISS from the Data Storage is Latitude: ${data.latitude} , Longitude: ${data.longitude}`
          );
          console.info("data", data);
        },
        (error) => {
          console.error(error);
        }
      );
    },
    showNotify(type, message) {
      this.client.interface.trigger("showNotify", {
        type: type,
        message: message,
      });
    },
  },
};
</script>

<style scoped>
.vue_logo {
  height: 40vmin;
  color: red;
}
</style>