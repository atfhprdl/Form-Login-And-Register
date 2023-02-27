<template>
  <div class="card-back">
    <div class="center-wrap pt-5 pb-5">
      <Form
        @submit="register"
        :validation-schema="registerFormSchema"
        :initialValues="formData"
        class="section text-center"
      >
        <h4 class="mb-4 pb-3">ثبت نام</h4>
        <div class="row">
          <div class="col-md-6">
            <div class="form-group">
              <Field
                type="text"
                class="form-style"
                placeholder="نام و نام خانوادگی"
                autocomplete="off"
                name="name"
              />
              <i class="input-icon uil uil-user"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="name" />
            </p>
          </div>
          <div class="col-md-6">
            <div class="form-group">
              <Field
                type="email"
                class="form-style"
                placeholder="ایمیل خود را وارد کنید"
                autocomplete="off"
                name="email"
              />
              <i class="input-icon uil uil-at"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="email" />
            </p>
          </div>

          <div class="col-md-6">
            <div class="form-group mt-2">
              <Field
                type="password"
                class="form-style"
                placeholder="کلمه عبور"
                autocomplete="off"
                name="password"
                :validateOnInput="true"
              />
              <i class="input-icon uil uil-lock-alt"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="password" />
            </p>
          </div>
          <div class="col-md-6">
            <div class="form-group mt-2">
              <Field
                type="password"
                class="form-style"
                placeholder="تکرار کلمه عبور"
                autocomplete="off"
                name="confirmPassword"
                :validateOnInput="true"
              />
              <i class="input-icon uil uil-lock-alt"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="confirmPassword" />
            </p>
          </div>
          <div class="col-md-6">
            <div class="form-group mt-2">
              <Field
                type="text"
                class="form-style"
                placeholder="شماره تلفن"
                name="phoneNumber"
                autocomplete="off"
                :validateOnInput="true"
              />
              <i class="input-icon uil uil-phone"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="phoneNumber" />
            </p>
          </div>
          <div class="col-md-6">
            <div class="form-group mt-2">
              <Field as="select" name="role" class="form-style">
                <option value="">نقش خود را انتخاب کنید</option>
                <option value="user">کاربر</option>
                <option value="student">دانشجو</option>
                <option value="teacher">مدرس</option>
              </Field>
              <i class="input-icon uil uil-rupee-sign"></i>
            </div>
            <p class="text-danger">
              <ErrorMessage name="role" />
            </p>
          </div>
          <div class="col-md-6">
            <div class="form-group mt-3" style="text-align: right">
              <label for="1">نامشخص</label>
              <Field
                type="radio"
                id="1"
                class="m-2"
                value="نامشخص"
                name="gender"
              />

              <label for="2">خانم</label>
              <Field
                type="radio"
                id="2"
                class="m-2"
                value="خانم"
                name="gender"
              />
              <label for="3">آقا</label>
              <Field
                type="radio"
                id="3"
                class="m-2"
                value="آقا"
                name="gender"
              />
            </div>
          </div>
        </div>
        <button class="btn mt-4">ثبت نام</button>
      </Form>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import { object, string, ref } from "yup";

export default {
  data() {
    const registerFormSchema = object({
      name: string().required("نام را وارد کنید"),
      email: string().required("ایمیل را وارد کنید").email("ایمیل نامعتبر است"),
      phoneNumber: string()
        .required("شماره تلفن را وارد کنید")
        .min(11, "شماره تلفن نامعتبر است")
        .max(11, "شماره تلفن نامعتبر است"),
      password: string()
        .required("کلمه عبور را وارد کنید")
        .min(6, "کلمه عبور باید بیشتر از 5 کاراکتر باشد"),
      confirmPassword: string()
        .required("تکرار کلمه عبور را وارد کنید")
        .oneOf([ref("password"), null], "کلمه های عبور یکسان نیستند"),
      role: string().required("نقش خود را انتخاب کنید"),
    });
    return {
      registerFormSchema,
      formData: {
        gender: "آقا",
        role: "user",
      },
    };
  },
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  methods: {
    register(values) {
      console.log(values);
    },
  },
};
</script>

<style></style>
