<template>
  <div class="webform">
    <form :id="formId" @submit.prevent="submitForm(formId)" novalidate>
      <h2>{{ title }}</h2>
      <div class="error" v-show="errorState">
        <p>
          It looks like you may have forgotten something. Please make sure you
          filled out all of the required fields.
        </p>
      </div>
      <div
        class="field"
        :class="{
          required: field.required,
          hasError: field.required && field.value.length == 0 && errorState,
        }"
        v-for="(field, i) in fields"
        :key="i"
      >
        <label class="wholeField" :for="field.id">{{ field.title }}</label>
        <input
          type="text"
          v-if="field.type == 'textInput'"
          :id="field.id"
          :ref="field.id"
          v-model="field.value"
          :required="field.required"
          :placeholder="field.placeholder"
        />
        <select
          v-else-if="field.type == 'select'"
          :id="field.id"
          :ref="field.id"
          v-model="field.value"
          :required="field.required"
        >
          <option
            v-for="option in field.options"
            :key="option.value"
            :value="option.value"
          >
            {{ option.name }}
          </option>
        </select>

        <div class="radioButtons" v-else-if="field.type == 'radioButtons'">
          <div
            class="radioButton option"
            v-for="button in field.options"
            :key="button.value"
          >
            <input
              type="radio"
              :id="button.name"
              :ref="button.name"
              :required="button.required"
              :name="field.variableName"
              v-model="field.value"
              :value="button.name"
            />
            <label class="radioLabel" :for="button.name">{{
              button.title
            }}</label>
          </div>
        </div>
        <div class="checkboxes" v-else-if="field.type == 'checkboxes'">
          <div
            class="checkbox option"
            v-for="button in field.options"
            :key="button.value"
          >
            <input
              type="checkbox"
              :id="button.name"
              :ref="button.name"
              :required="button.required"
              :name="field.variableName"
              v-model="field.value"
              :value="button.name"
            />
            <label class="checkboxLabel" :for="button.name">{{
              button.title
            }}</label>
          </div>
        </div>
      </div>
      <button type="submit" :form="formId">
        <Icon v-if="icon" :icon="icon" /> {{ submitText }}
      </button>
    </form>
  </div>
</template>

<script>
import { Icon } from "@iconify/vue2";
export default {
  name: "Webform",
  components: { Icon },
  props: {
    title: String,
    formId: String,
    fields: Array,
    icon: String,
    submitText: String,
    submitAction: Function,
  },
  data() {
    return {
      errorState: false,
    };
  },
  methods: {
    submitForm() {
      let foundError = false;
      this.fields.forEach((field) => {
        if (field.required && field.value.length == 0) {
          foundError = true;
        }
      });
      if (foundError) {
        window.scrollTo({ top: 0, behavior: "smooth" });
        this.errorState = true;
      } else {
        this.submitAction();
      }
    },
  },
};
</script>

<style lang="scss">
.webform {
  width: 100%;
  max-width: 560px;
  border-radius: 12px;
  background: #fff;
  padding: 1.5em;
  box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.42);
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 2em;
  h2 {
    margin-top: 0;
    font-weight: 400;
    color: #0d3b66;
    margin-bottom: 0.5em;
    text-align: center;
  }
  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    .field {
      margin: 0.75em 0;
      width: 100%;
      max-width: 340px;
      transition: all ease 300ms;
      &.required {
        &.hasError {
          background: #f95738;
          color: #fff;
          padding: 1em;
          border-radius: 12px;
          padding-bottom: 1.5em;
          label.wholeField::after {
            color: #fff;
            content: " – This field is required.";
            font-size: 0.75em;
          }
        }
        label.wholeField::after {
          content: " *";
          color: #f95738;
        }
      }
      label.wholeField {
        display: block;
        margin-bottom: 0.25em;
        font-weight: 400;
      }
      input[type="text"] {
        font-weight: 200;
        width: 100%;
        padding: 0.25em 0.5em;
        border: solid 0.5px #222;
        border-radius: 6px;
      }
      select {
        font-weight: 300;
      }
      .option {
        input {
          margin-right: 0.25em;
        }
      }
    }
    .error {
      color: #f95738;

      p {
        margin-top: 0;
        font-weight: 400;
      }
      ul {
        margin: 0.5em 0 0 0;
      }
    }
    button {
      background: #f4d35e;
      border: none;
      border-radius: 12px;
      padding: 0.5em 1em;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 500;
      width: 100%;
      max-width: 340px;
      text-align: center;
      margin-top: 1.5em;
      svg {
        margin-right: 5px;
      }
    }
  }
}
</style>
