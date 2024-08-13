<template>
  <div>
    <h1>Api con page</h1>
    <v-row>
      <v-col cols="12">
        <v-btn color="success" @click="newItem()">newItem</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="3" v-for="(item, index) in apidata" :key="index">
        <v-card width="300">
          <v-img
            width="300"
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQSN5kyGXRsJTnCvfM371Ycg8u7k9viw1gW-g&s"
          ></v-img>
          <v-card-title primary-title>
            {{ item.username }}
            {{ item.email }}
            {{ item.is_approve }}
          </v-card-title>
          <v-card-action>
            <v-btn color="success" @click="editItem(item)">Edit</v-btn>
            <v-btn color="error" @click="deleteItem(item)">Delete</v-btn>
          </v-card-action>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="dialogedit" max-width="500px">
      <v-card>
        <v-card-title primary-title> {{ savemode }} </v-card-title>
        <v-card-text>
          <v-row>
            <v-col cols="6">
              <v-text-field
                name="username"
                label="username"
                id="id"
                v-model="postdata.username"
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                name="password"
                label="password"
                id="id"
                v-model="postdata.password"
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                name="email"
                label="email"
                id="id"
                v-model="postdata.email"
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-text-field
                name="role"
                label="role"
                id="id"
                v-model="postdata.role"
              ></v-text-field>
            </v-col>
            <v-col cols="4">
              <v-text-field
                name="firstname"
                label="firstname"
                id="id"
                v-model="postdata.user_info.firstname"
              ></v-text-field>
            </v-col>
            <v-col cols="4">
              <v-text-field
                name="lastname"
                label="lastname"
                id="id"
                v-model="postdata.user_info.lastname"
              ></v-text-field>
            </v-col>
            <v-col cols="4">
              <v-text-field
                name="gender"
                label="gender"
                id="id"
                v-model="postdata.user_info.gender"
              ></v-text-field>
            </v-col>
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text color="error" @click="closeItem()">cancel</v-btn>
          <v-btn text color="info" @click="saveSelect()">save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  name: "apicon",
  data() {
    return {
      id: "",
      apidata: [],
      dialogedit: false,
      postdata: {
        username: "",
        password: "",
        email: "",
        role: "",
        user_info: {
          firstname: "",
          lastname: "",
          gender: "",
        },
        is_approve: false,
      },
      postdefault: {
        username: "",
        password: "",
        email: "",
        role: "",
        user_info: {
          firstname: "",
          lastname: "",
          gender: "",
        },
        is_approve: false,
      },
    };
  },
  created() {
    this.setToken();
    if (localStorage.getItem("Token") != undefined) {
      this.getData();
    }
  },
  computed: {
    savemode() {
      return this.id == "" ? "New Item" : "Edit Item";
    },
  },
  methods: {
    newItem() {
      this.id = "";
      this.postdata = { ...this.postdefault };
      this.dialogedit = true;
    },
    editItem(item) {
      this.id = item._id;
      this.postdata = { ...item };
      this.dialogedit = true;
    },
    closeItem() {
      this.id = "";
      this.postdata = { ...this.postdefault };
      this.dialogedit = false;
    },
    saveSelect() {
      if (this.id != "") {
        this.savePutData();
      } else {
        this.savePostData();
      }
    },
    setToken() {
      localStorage.setItem(
        "Token",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY2YjMyMzlkYmRlYTE0Y2ZiZWJjOGE5YiIsInVzZXJuYW1lIjoiYWRtaW4xIiwicm9sZSI6ImFkbWluIiwiaWF0IjoxNzIzNTQzMjI2fQ.QYRcLvemYLcDkYlPqRJAkAtxqu7EvPRPOOyJ8v6ExiA"
      );
    },
    getData() {
      this.axios
        .get("http://localhost:3000/api/v1/users/", {
          headers: {
            Authorization: `Bearer ${localStorage.getItem("Token")}`,
          },
        })
        .then((response) => {
          console.log(response.data);
          this.apidata = response.data.data;
          console.log(this.apidata);
        });
    },
    async savePostData() {
      try {
        const { data } = await this.axios.post(
          "http://localhost:3000/api/v1/register",
          this.postdata,
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem("Token")}`,
            },
          }
        );
        console.log(data);
        alert("Create Complete");
        this.getData();
        this.closeItem();
      } catch (error) {
        console.log(error);
        alert("Error จ้า");
      }
    },
    async savePutData() {
      try {
        const { data } = await this.axios.put(
          "http://localhost:3000/api/v1/approve/" + this.id,
          { is_approve: true },
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem("Token")}`,
            },
          }
        );
        console.log(data);
        alert("Update Complete");
        this.getData();
        this.closeItem();
      } catch (error) {
        console.log(error);
        alert("Error จ้า");
      }
    },
    async deleteItem(item) {
      if (confirm("delete" + this.username)) {
        try {
          const { data } = await this.axios.delete(
            "http://localhost:3000/api/v1/users/" + item._id,
            {
              headers: {
                Authorization: `Bearer ${localStorage.getItem("Token")}`,
              },
            }
          );
          console.log(data);
          alert("Delete Complete");
          this.getData();
          this.closeItem();
        } catch (error) {
          console.log(error);
          alert("Error จ้า");
        }
      }
    },
  },
};
</script>

<style>
</style>