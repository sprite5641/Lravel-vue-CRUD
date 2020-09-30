<template>
  <div class="my-form">
    <form class="ui form">
      <div class="fields">
        <div class="four wide field">
          <label>ชื่อ</label>
          <input
            type="text"
            name="first_name"
            placeholder="ชื่อ"
            @change="handleChange"
            :value="form.first_name"
          />
        </div>

        <div class="four wide field">
          <label>นามสกุล</label>
          <input
            type="text"
            name="last_name"
            placeholder="นามสกุล"
            @change="handleChange"
            :value="form.last_name"
          />
        </div>

        <div class="six wide field">
          <label>อีเมลล์</label>
          <input
            type="email"
            name="email"
            placeholder="ป้อนอีเมลล์"
            @change="handleChange"
            :value="form.email"
          />
        </div>
        <div class="two wide field">
          <button :class="btnClass" @click="onFormSubmit">
            {{ btnName }}
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "MyForm",
  data() {
    return {
      btnName: "บันทึก",
      btnClass: "ui primary button submit-button",
    };
  },
  props: {
    form: {
      type: Object,
    },
  },
   methods: {
    handleChange(event) {
      const { name, value } = event.target;
      let form = this.form;
      form[name] = value;
      this.form = form;
    },
    onFormSubmit(event) {
      // prevent form submit
      event.preventDefault();

      // form validation
      if (this.formValidation()) {
        // window.console.log("ready to submit");
        this.$emit("onFormSubmit", this.form);

        // change the button to save
        this.btnName = "Save";
        this.btnClass = "ui primary button submit-button";

        // clear form fields
        this.clearFormFields();
      }
    },
    formValidation() {
      // first name
      if (document.getElementsByName("first_name")[0].value === "") {
        alert("Enter first name");
        return false;
      }

      // last name
      if (document.getElementsByName("last_name")[0].value === "") {
        alert("Enter last name");
        return false;
      }

      // email
      if (document.getElementsByName("email")[0].value === "") {
        alert("Enter email");
        return false;
      }

      return true;
    },
    clearFormFields() {
      // clear form data
      this.form.first_name = "";
      this.form.last_name = "";
      this.form.email = "";
      this.form.isEdit = false;

      // clear form fields
      document.querySelector(".form").reset();
    }
  },
   updated() {
    if (this.form.isEdit) {
      this.btnName = "Update";
      this.btnClass = "ui orange button submit-button";
    }
  }
};
</script>


<style scoped>
</style>
