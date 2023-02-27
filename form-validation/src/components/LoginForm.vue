<template>
  <div class="card-front">
    <div class="center-wrap">
      <Form
        @submit="login"
        class="section text-center"
        :validation-schema="loginFormSchema"
      >
        <h4 class="mb-4 pb-3">ورود</h4>
        <div class="form-group">
          <Field
            type="text"
            class="form-style"
            placeholder="ایمیل خود را وارد کنید"
            autocomplete="off"
            name="email"
            :validateOnInput="true"
          />
          <i class="input-icon uil uil-at"></i>
        </div>
        <p class="text-danger">
          <ErrorMessage name="email" />
        </p>
        <div class="form-group mt-2">
          <Field
            type="password"
            class="form-style"
            placeholder="پسورد را وارد کنید"
            autocomplete="off"
            name="password"
            :validateOnInput="true"
          />
          <i class="input-icon uil uil-lock-alt"></i>
        </div>
        <p class="text-danger">
          <ErrorMessage name="password" />
        </p>
        <button class="btn mt-4">ورود به سایت</button>
        <p class="mb-0 mt-4 text-center">
          <a href="#0" class="link">آیا کلمه عبور خود را فراموش کرده اید ؟</a>
        </p>
      </Form>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import { object, string } from "yup";
export default {
  name: "LoginForm",
  components: { Form, Field, ErrorMessage },
  data() {
    const loginFormSchema = object({
      email: string().required("ایمیل را وارد کنید").email("ایمیل نامعتبر است"),
      password: string()
        .required("کلمه عبور را وارد کنید")
        .min(6, "کلمه عبور باید بیشتر از 5 کاراکتر باشد"),
    });
    return {
      loginFormSchema,
    };
  },
  methods: {
    login(values) {
      console.log(values);
    },
  },
};
</script>

<style></style>
