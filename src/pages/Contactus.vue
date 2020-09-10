<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="8" offset-sm="2">
          <!-- <v-card> -->
          <v-card-title class="text-h4 font-weight-light pl-0"
            >Contact us</v-card-title
          >
          <v-form
            ref="form"
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
              v-model="formData.name"
              :error-messages="nameErrors"
              :counter="10"
              label="Name"
              required
              @input="$v.name.$touch()"
              @blur="$v.name.$touch()"
            ></v-text-field>
            <v-text-field
              v-model="formData.email"
              :error-messages="emailErrors"
              label="E-mail"
              required
              @input="$v.email.$touch()"
              @blur="$v.email.$touch()"
            ></v-text-field>
            <v-btn class="mr-4" @click="submit">submit</v-btn>
            <v-btn @click="clear">clear</v-btn>
          </v-form>
          <!-- <v-form
            ref="form"
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
              filled
              v-model="formData.name"
              :counter="10"
              :rules="nameRules"
              placeholder="John"
              name="name"
              label="Name"
              required
            ></v-text-field>
            <v-text-field
              solo-inverted
              color="amber"
              v-model="formData.email"
              :rules="emailRules"
              placeholder="Smith"
              name="email"
              label="Email"
              required
            ></v-text-field>
            <v-textarea
              filled
              clearable
              auto-grow
              no-resize
              :rules="messageRules"
              placeholder="Hello!"
              v-model="formData.message"
              name="message"
              label="Message"
            ></v-textarea>
            <v-btn class="amber darken-1 black--text" type="submit">Submit</v-btn>
            <v-btn color="white--text" text class="mr-l" @click="reset">Clear</v-btn>
          </v-form>-->
          <!-- </v-card> -->
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, maxLength, email } from "vuelidate/lib/validators";

export default {
  name: "Contact",
  mixins: [validationMixin],

  validations: {
    name: { required, maxLength: maxLength(10) },
    email: { required, email }
  },

  data: () => ({
    formData: {},
    name: "",
    email: ""
  }),

  computed: {
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 10 characters long");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    }
  },

  methods: {
    submit() {
      this.$v.$touch();
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.email = "";
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
          ...this.formData
        })
      })
        .then(() => this.$router.push("/"))
        .catch((error) => alert(error));
    }
  }
};
</script>
// export default { // name: "Contact", // data() { // return { // valid: true,
// name: "", // nameRules: [ // (v) => !!v || "Name is required", // (v) => (v
&& v.length <= 10) || "Name must be less than 10 characters", // ], // email:
"", // emailRules: [ // (v) => !!v || "E-mail is required", // (v) =>
/.+@.+\..+/.test(v) || "E-mail must be valid", // ], // message: "", //
messageRules: [ // (v) => !!v || "Message is required", // (v) => (v && v.length
<= 250) || "Send us your thoughts and feedback", // ], // formData: {}, // }; //
}, // methods: { // reset() { // this.$refs.form.reset(); // }, // encode(data)
{ // return Object.keys(data) // .map( // (key) => encodeURIComponent(key) + "="
+ encodeURIComponent(data[key]) // ) // .join("&"); // }, // handleSubmit(e) {
// fetch("/", { // method: "POST", // headers: { "Content-Type":
"application/x-www-form-urlencoded" }, // body: this.encode({ // "form-name":
e.target.getAttribute("name"), // ...this.formData, // }), // }) // .then(() =>
this.$router.push("/")) // .catch((error) => alert(error)); // }, // }, // }; //
