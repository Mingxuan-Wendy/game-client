<template>
  <div class="main_container">
    <div class="r_container">
      <el-card class="box-card" style="border-radius: 10%">
        <div class="sign">
          <p class="sign_in">Sign in</p>
          <div class="create">
            <p>New user? </p>
            <p class="register" style="text-decoration: underline;" @click="clickToRegister">Create an account</p>
          </div>
        </div>
        <el-form
          :label-position="labelPosition"
          ref="form"
          label-width="80px"
          :model="form"
        >
          <!-- 做校验需要ref prop等 -->
          <el-form-item
            label="Username"
            prop="username"
            style="text-align: left; margin-left: 50px"
          >
            <el-input v-model="form.username" style="width: 300px"></el-input>
          </el-form-item>
          <el-form-item
            label="password"
            prop="password"
            style="text-align: left; margin-left: 50px"
          >
            <el-input
              type="password"
              v-model="form.password"
              style="width: 300px"
            ></el-input>
          </el-form-item>
          <el-form-item style="margin-left: 50px">
            <el-button type="success" style="width: 300px" @click="clickContinue">Continue</el-button>
          </el-form-item>
          <div class="continue" style="text-align: center; margin-left: 0px">
            Or continue with
          </div>
          <el-form-item style="margin-left: 50px">
            <router-link :to="{ name: 'HomeContent' }">
              <el-button type="primary" style="width: 300px">Default User</el-button>
            </router-link>
          </el-form-item>
        </el-form>
      </el-card>
    </div>

    <div class="l_container">
      <div class="logo">
        <i>BGMT</i>
        BGMT
      </div>
      <div class="r_footer">
        <p class="cue">You may also like:</p>
        <div class="first">
          <img src="../../assets/imgs/test.jpg" alt="" class="img1" />
          <div class="info1">
            <div>league of Legends111</div>
            <div>league of Legends</div>
            <div><span>icon</span>8.6</div>
          </div>
        </div>
        <div class="second">
          <img src="../../assets/imgs/test.jpg" alt="" class="img2" />
          <div class="info2">
            <div>league of Legends222</div>
            <div>league of Legends</div>
            <div><span>icon</span>8.6</div>
          </div>
        </div>
        <div class="third">
          <img src="../../assets/imgs/test.jpg" alt="" class="img3" />
          <div class="info3">
            <div>league of Legends333</div>
            <div>league of Legends</div>
            <div><span>icon</span>8.6</div>
          </div>
        </div>
        <div class="fourth">
          <i>icon</i>
          Discover more
        </div>
      </div>
    </div>
    <el-dialog :visible.sync="dialogVisible" width="60%" height="500px">
      <Register></Register>
    </el-dialog>
  </div>
</template>

<script>
import Register from "../../components/login/register.vue"
import axios from "axios";
export default {
  components: {
    Register,
  },

  data() {
    return {
      labelPosition: "top",
      form: {
        username: "",
        password: "",
      },
      dialogVisible: false,
      userData: {},
    };
  },
  methods: {
    clickToRegister() {
      this.dialogVisible = true;
    },
    async clickContinue() {
      const response = await axios.get("http://127.0.0.1:8000/api/custom_user/users/");
      const users = response.data;
      let userId;
      for(var i=0; i<users.length; i++){
        if(this.form.username === users[i]["email"] && this.form.password === users[i]["password"]) {
          userId = users[i]["id"];
          break;
        }
      }
      await this.$router.push({
        name: 'HomeContent',
        params: {
          user_id: userId,
        }
      });

    },
  },
};
</script>

<style lang="scss" scoped>
.main_container {
  background: url("../../assets/imgs/login.jpg") no-repeat;
  background-size: 100% 100%;
  height: 100vh;
}

.r_container {
  float: left;
  height: 500px;
  width: 450px;
  // background-color: aquamarine;
  position: absolute;
  top: 15%;
  left: 55%;
}

.l_container {
  float: right;
  height: 500px;
  width: 450px;
  // background-color: bisque;
  position: absolute;
  top: 15%;
  right: 55%;
}

// .continue{
//   text-align: left;
// }

.continue {
  margin-left: 50px;
  text-align: left;
}

.sign {
  margin-left: 50px;
  text-align: left;
}

.sign_in {
  font-family: "Helvetica Neue";
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 20px;
  margin-top: 10px;
  // color: rgb(96,98,102);
}

.create {
  display: flex;
}
.register {
  cursor: pointer;
  margin-left: 10px;
}
.create,
.continue {
  margin-bottom: 20px;
  font-family: "Helvetica Neue";
  font-size: 90%;
  font-weight: 400;
  color: rgb(96, 98, 102);
}

.logo {
  font-family: "Helvetica Neue";
  font-size: 30px;
  font-weight: 700;
  margin-bottom: 20px;
  margin-top: 30px;
  margin-left: 50px;
  text-align: left;
  color: rgb(208, 211, 217);
}

.cue {
  margin-right: 224px;
  margin-bottom: 20px;
  color: rgb(208, 211, 217);
}
.first,
.second,
.third {
  position: relative;
  width: 245px;
  height: 80px;
  background-color: rgba(1, 1, 1, 0.4);
  text-align: left;
  margin-left: 50px;
  margin-bottom: 20px;
  border-radius: 10px;
}
.fourth {
  text-align: left;
  margin-left: 50px;
  font-size: small;
  font-weight: 600;
  color: rgb(249, 250, 251);
}

.img1,
.img2,
.img3 {
  width: 70px;
  height: 80px;
  float: left;
  position: absolute;
  border-radius: 10px;
}
.info1,
.info2,
.info3 {
  text-align: left;
  float: left;
  position: absolute;
  left: 100px;
  font-size: small;
  color: rgb(208, 211, 217);
  div {
    margin-top: 3px;
    margin-bottom: 10px;
  }
  :nth-child(3) {
    background-color: rgb(255, 117, 75);
    text-align: center;
    line-height: 20px;
    width: 60px;
    height: 20px;
    color: white;
    border-radius: 10px;
  }
}
</style>
