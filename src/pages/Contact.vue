<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <p class="text-h5 font-weight-light grey--text mb-5">/Contact</p>
          <v-card class="pa-4">
            <p class="text-overline font-weight-light">Contact us</p>

            <v-form
              autocomplete="off"
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
                dense
                background-color="grey darken-3"
                color="orange accent-2"
                append-icon="mdi-face"
                type="text"
                name="name"
                v-model="formData.name"
                :rules="nameRules"
                label="Your name"
              />

              <v-text-field
                solo
                dense
                background-color="grey darken-3"
                color="orange"
                append-icon="mdi-email"
                type="email"
                name="email"
                v-model="formData.email"
                :rules="emailRules"
                label="Email address"
              />

              <v-textarea
                solo
                background-color="grey darken-3"
                color="orange"
                append-icon="mdi-comment"
                name="message"
                v-model="formData.message"
                :rules="messageRules"
                label="Message here..."
                auto-grow
                no-resize
                clearable
                :counter="200"
              ></v-textarea>

              <v-btn
                color="orange black--text"
                :disabled="!valid"
                type="submit"
                @click="validate"
                class="mr-4"
              >Send</v-btn>
              <v-btn @click="reset">Clear</v-btn>
            </v-form>
          </v-card>
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
          (v && v.length <= 200) || "Message must be less than 200 characters",
      ],
    };
  },
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
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
