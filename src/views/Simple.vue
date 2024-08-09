<template>
  <div>
    <h1>Simple Page</h1>
    <h1 v-if="show">{{ name }}</h1>
    <v-btn color="success" @click="show = !show">switch</v-btn>
    <v-row>
      <v-col cols="3" v-for="(item, index) in catlist" :key="index">
        <v-card width="300">
          <v-img width="300" :src="item.imglink"></v-img>
          <v-card-title primary-title>
            {{ item.name }}
          </v-card-title>
          <v-card-action>
            <v-btn color="success" @click="callAlertParam(item.name)"
              >Call Alert</v-btn
            >
          </v-card-action>
        </v-card>
      </v-col>
      <v-col cols="12">
        <h1>Message: {{ message }}</h1>
        <v-text-field
          name="message"
          label="message"
          id="message"
          v-model="message"
        ></v-text-field>
        <v-btn color="success" @click="callAlertParam(message)"
          >Alert message</v-btn
        >
      </v-col>
      <v-col cols="12">
        <v-btn color="success" @click="callAlert()">call alert</v-btn>
        <v-btn color="success" @click="removeLocal()">Remove Local</v-btn>
      </v-col>
      <v-col cols="12">
        <subcom
          :name="name"
          @callAlert="callAlert"
          @callAlertParam="callAlertParam"
        />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import subcom from "../components/SubCom";
import { EventBus } from "@/EventBus";
export default {
  components: {
    subcom,
  },
  data() {
    return {
      message: "",
      name: "Thid",
      show: false,
      catlist: [
        {
          name: "foo",
          imglink:
            "https://www.wfla.com/wp-content/uploads/sites/71/2023/05/GettyImages-1389862392.jpg?w=2560&h=1440&crop=1",
        },
        {
          name: "bar",
          imglink:
            "https://i.natgeofe.com/n/4cebbf38-5df4-4ed0-864a-4ebeb64d33a4/NationalGeographic_1468962.jpg",
        },
      ],
    };
  },
  methods: {
    callAlert() {
      alert("Kittens");
    },
    callAlertParam(item) {
      // Set Local Storage
      localStorage.setItem("User", item);
      // Set Cookies
      this.$cookies.set("token", item, "30s");
      alert(item);
    },
    removeLocal() {
      localStorage.removeItem("User");
      alert("Remove complete");
    },
  },
  mounted() {
    EventBus.$on("callAlert", this.callAlert);
    EventBus.$on("callAlertParam", this.callAlertParam);
  },
  beforeDestroy() {
    EventBus.$off("callAlert", this.callAlert);
    EventBus.$off("callAlertParam", this.callAlertParam);
  },
};
</script>

<style>
</style>