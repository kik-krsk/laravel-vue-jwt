<template>
  <div class="w-25">
    <input
      v-model="name"
      type="text"
      class="form-control mt-3 mb-3"
      placeholder="name"
    />
    <input
      v-model="email"
      type="email"
      class="form-control mb-3"
      placeholder="email"
    />
    <input
      v-model="password"
      type="password"
      class="form-control mb-3"
      placeholder="password"
    />
    <input
      v-model="password_confirmation"
      type="password"
      class="form-control mb-3"
      placeholder="confirm password"
    />
    <div v-if="error" class="text-danger">{{ this.error }}</div>

    <input
      @click.prevent="store"
      type="submit"
      value="Submit"
      class="btn btn-primary"
    />
  </div>
</template>

<script>
export default {
  name: "Registration",

  data() {
    return {
      name: "",
      email: "",
      password: "",
      password_confirmation: "",
      error: null,
    };
  },
  mounted() {
    localStorage.getItem("access_token");
  },
  methods: {
    store() {
      axios
        .post("/api/users", {
          name: this.name,
          email: this.email,
          password: this.password,
          password_confirmation: this.password_confirmation,
        })
        .then((res) => {
          localStorage.setItem("access_token", res.data.access_token);
          this.$router.push({ name: "user.personal" });
        })
        .catch((error) => {
          this.error = error.response.data.error;
        });
    },
  },
};
</script>
