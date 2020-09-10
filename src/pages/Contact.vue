<template>
  <Layout>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <div class="text-h4 font-weight-light mb-5">Contact us</div>
          <v-form
            ref="form"
            v-model="valid"
            name="contact"
            method="post"
            v-on:submit.prevent="validate_submit(e)"
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
            ></v-textarea>

            <v-btn :disabled="!valid" type="submit">Submit form</v-btn>
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
    encode(data) {
      return Object.keys(data)
        .map(
          (key) => encodeURIComponent(key) + "=" + encodeURIComponent(data[key])
        )
        .join("&");
    },
    validate_submit(e) {
      if (this.$refs.form.validate()) {
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
      }
    },
  },
};
</script>
