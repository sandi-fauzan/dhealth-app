<template>
  <div class="home">
    <h1>Login</h1>
    <h4>Login Untuk Melihat History</h4>

    <div class="main">
      <form @submit.prevent="login()">
        <input
          type="email"
          v-model="email"
          placeholder="Masukan Email Kamu"
          required
        />

        <div class="submit">
          <input type="submit" value="LOGIN" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      email: "",
      key: "",
    };
  },
  methods: {
    async login() {
      try {
        await axios
          .get("https://soal-rekrutmen.dhealth.co.id/test/v1/get-key", {
            headers: {
              "Content-Type": "application/json",
            },
            params: { email: this.email },
          })
          .then(
            (res) => (this.key = res.data.key)
             this.$router.push({
               name: "history",
               headers: {
                 "x-api-key": this.key,
                 "x-api-token": `base64_encode(${this.email}:${this.key})`,
                 "Content-Type": "application/json",
               },
             }),
          );
        alert("sukses login");
      } catch (err) {
        this.$router.push("/");
        console.log(this.email);
        this.error = err.response.data;
        console.log(this.error);
        console.log(this.email);
        console.log(this.res.data.key);
      }
    },
  },
};
</script>

<style scoped>
.home {
  width: 100%;
}
.main {
  width: 45%;
  padding: 60px 100px;
  border-radius: 20px;
  background: rgb(244, 244, 244);
  margin: 60px auto;
}

.main form input[type="email"] {
  width: 80%;
  padding: 18px 24px;
  border-radius: 30px;
  border: none;
  outline: none;
  background: white;
  box-shadow: 1px 8px 16px 2px rgba(189, 189, 189, 0.293);
}

.main form input[type="submit"] {
  width: 50%;
  margin-top: 30px;
  padding: 15px 24px;
  border-radius: 30px;
  border: none;
  outline: none;
  background: rgb(155, 24, 231);
  color: white;
  font-weight: 800;
  transition: 0.5s;
  cursor: pointer;
}

.main form input[type="submit"]:hover {
  background: rgb(119, 12, 180);
  transform: scale(1.05);
  box-shadow: 1px 8px 16px 2px rgba(189, 189, 189, 0.293);
}
</style>
