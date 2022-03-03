<template>
  <div>
    <button @click="registerUser()">register user</button>
    <button @click="loadDatas()">load datas</button>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      register: {
        email: "mueen@gmail.com",
        password: "azerty",
        password_confirmation: "azerty",
      },
    };
  },
  methods: {
    loadDatas() {
      this.$axios.post("/meds/loadMeds");
    },
    registerUser() {
      this.$axios
        .post("/user/register", this.register)
        .then((response) => {
          console.log(response);
          this.$auth.loginWith("local", {
            data: {
              email: this.register.email,
              password: this.register.password,
            },
          });
        })
        .catch((err) => {
          this.error = err.response.data;
        });
    },
  },
};
</script>
