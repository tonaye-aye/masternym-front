<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <div class="text-h5 font-weight-light mb-5">Contact us</div>
          <v-form
            ref="form"
            name="contact"
            method="post"
            v-on:submit.prevent="handleSubmit"
            v-model="valid"
            action="/thanks/"
            data-netlify="true"
            data-netlify-honeypot="bot-field"
          >
            <input type="hidden" name="form-name" value="contact" />
            <p hidden>
              <label>
                Don’t fill this out:
                <input name="bot-field" />
              </label>
            </p>

            <v-text-field
              solo
              type="text"
              name="name"
              v-model="formData.name"
              :rules="nameRules"
              label="Name"
            />

            <v-text-field
              solo
              type="email"
              name="email"
              v-model="formData.email"
              :rules="emailRules"
              label="Email"
            />

            <v-textarea
              solo
              name="message"
              v-model="formData.message"
              :rules="messageRules"
              label="Message"
              auto-grow
              no-resize
              clear-icon
              color="white"
            ></v-textarea>

            <v-btn :disabled="!valid" type="submit" @click="validate">Submit form</v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Contact us",
  },
  data() {
    return {
      formData: {},
      valid: true,
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
      ],
      emailRules: [
        (v) => !!v || "Email is required",
        (v) => /.+@.+\..+/.test(v) || "Email must be valid",
      ],
      messageRules: [
        (v) => !!v || "Message is required",
        (v) =>
          (v && v.length <= 250) || "Message must be less than 250 characters",
      ],
    };
  },
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => encodeURIComponent(key) + "=" + encodeURIComponent(data[key])
        )
        .join("&");
    },
    handleSubmit(e) {
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": e.target.getAttribute("name"),
          ...this.formData,
        }),
      })
        .then(() => this.$router.push("/thanks"))
        .catch((error) => alert(error));
    },
  },
};
</script>
