<template>
  <div class="register">
    <div class="userName">
      <p>User name: </p>
      <el-input class="input" v-model="inputUserName" placeholder="Please input user name you want to use for register."></el-input>
    </div>
    <div class="email">
      <p>Email: </p>
      <el-input class="input" v-model="email" placeholder="Please input your email address."></el-input>
    </div>
    <div class="password">
      <p>Password:</p>
      <el-input class="input" type="password" v-model="inputPassword1" placeholder="Please set your user password here."></el-input>
    </div>
    <div class="password">
      <p>Confirm Password:</p>
      <el-input class="input" type="password" v-model="inputPassword2" placeholder="Please confirm your password here."></el-input>
    </div>
    <div class="submit">
    <el-button @click="submitRegister">Submit</el-button>
  </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: '',
      inputUserName: '',
      inputPassword1: '',
      inputPassword2: ''
    }
  },
  methods: {
    async submitRegister() {
      if(this.inputPassword1 !== this.inputPassword2) {
        alert("The password you entered for initialize and confirm do not match!");
      }
      const data = {
        nickname: this.inputUserName,
        username: this.inputUserName,
        email: this.email,
        password: this.inputPassword1,
      }
      const registerResponse = await axios.post("http://127.0.0.1:8000/api/custom_user/users/", data);
      const status = registerResponse.status;
      if(status === 201) {
        window.location.reload();
      }else {
        alert("Register failed, you can also try to login as Default User!");
      }
    },
  },
}
</script>

<style scoped>
.register {
  display: flex;
  flex-direction: column;
}
.userName, .email {
  display: flex;
}
.userName p {
  width: 15%;
}
.email p {
  width: 15%;
}
.password p {
  width: 15%;
}
.password {
  display: flex;
}
.input {
  margin-left: 20px;
}
.submit {
  float: right;
  margin-left: 90%;
}
</style>