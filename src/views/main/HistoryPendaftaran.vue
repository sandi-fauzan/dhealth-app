<template>
  <div class="home">
    <h1>History Pendaftaran</h1>
    <p>{{ key }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "History Pendaftaran",
  props: ["key", "email"],
  data() {
    // return {
    //   email: this.email,
    //   key: this.key,
    // };
  },
  methods: {
    async getHistoryPendaftaran() {
      try {
        await axios
          .get("https://soal-rekrutmen.dhealth.co.id/test/v1/list-history", {
            headers: {
              "x-api-key": this.key,
              "x-api-token": `base64_encode(${this.email}:${this.key})`,
              "Content-Type": "application/json",
            },
          })
          .then((res) => console.log(res.data));
        alert("sukses masuk halaman pendaftaran");
      } catch (err) {
        // this.$router.push("/");
        console.log(this.email);
        this.error = err.response.data;
        console.log(this.error);
        console.log(this.key);
        console.log(this.email);
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
  margin: 100px auto;
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