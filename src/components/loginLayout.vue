<template>
  <v-app>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="8" md="8">
            <v-card>
              <v-row>
                <v-col cols="6">
                  <div class="header">
                    <div id="title">Silahkan Login Untuk Masuk</div>
                    <div id="tagline">HumanTech Corporations</div>
                  </div>
                  <div class="form">
                    <v-text-field label="Email" v-model="form.email" outlined height="54"></v-text-field>
                    <v-text-field
                      label="Password"
                      v-model="form.password"
                      type="password"
                      outlined
                      height="54"
                    ></v-text-field>

                    <v-checkbox v-model="checkbox" color="primary">
                      <template v-slot:label>
                        <div>
                          Forgot Password ?
                          <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                              <a
                                target="_blank"
                                href="http://vuetifyjs.com"
                                @click.stop
                                v-on="on"
                              >Click Here To Continue</a>
                            </template>
                            Opens in new window
                          </v-tooltip>.
                        </div>
                      </template>
                    </v-checkbox>
                    <v-btn @click="login()" color="indigo" class="elevation-0" dark>LOG IN NOW</v-btn>
                  </div>
                </v-col>
                <v-col cols="6" md="6" style="padding:0px">
                  <v-img :src="require('@/assets/Mask.svg')"></v-img>
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: null,
        password: null
      },
      user: new FormData()
    };
  },
  methods: {
    login() {
      var url = this.$apiUrl + "/auth";
      this.user = new FormData();
      this.user.append("email", this.form.email);
      this.user.append("password", this.form.password);
      this.user = new FormData();
      this.$http.post(url, this.user).then(response => {
        if (!response.data.token) {
          localStorage.setItem("token", response.data.token);
          this.$router.push({ name: "UserController" });
        } else {
          alert("gagal login");
        }
      });
    }
  }
};
</script>

<style>
.form {
  margin-left: 39px;
  margin-top: 94.5px;
  margin-right: 68px;
  margin-bottom: 33.75px;
}
.header {
  margin-left: 39px;
  margin-top: 27px;
}
#title {
  font-family: Gothic A1;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 45px;
}

#tagline {
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 28px;
}
</style>