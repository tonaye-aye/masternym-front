<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="8" offset-sm="2">
          <!-- <v-card> -->
          <v-card-title class="text-h3">Contact us</v-card-title>
          <v-form
            ref="form"
            v-model="valid"
            lazy-validation
            name="contact"
            method="post"
            v-on:submit.prevent="handleSubmit"
            action="/"
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
              v-model="formData.name"
              :counter="10"
              :rules="nameRules"
              label="Name"
              required
            ></v-text-field>
            <v-text-field solo v-model="formData.email" :rules="emailRules" label="E-mail" required></v-text-field>
            <v-textarea
              solo
              clearable
              auto-grow
              no-resize
              :rules="messageRules"
              placeholder="Message here..."
              v-model="formData.message"
              name="message"
              label="Message"
            ></v-textarea>
            <v-btn color="success" type="submit" class="mr-4">Submit</v-btn>
            <v-btn color="error" class="mr-4" @click="reset">Reset</v-btn>
          </v-form>
          <!-- </v-card> -->
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<script>
export default {
  name: "Contact",
  data() {
    return {
      valid: true,
      name: "",
      nameRules: [
        (v) => !!v || "Name is required",
        (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
      ],
      email: "",
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
      ],
      message: "",
      messageRules: [
        (v) => !!v || "Message is required",
        (v) => (v && v.length <= 250) || "Send us your thoughts and feedback",
      ],
      formData: {},
    };
  },
  methods: {
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
        .then(() => this.$router.push("/"))
        .catch((error) => alert(error));
    },
  },
};
</script>
