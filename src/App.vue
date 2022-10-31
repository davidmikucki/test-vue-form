<template>
  <div id="app">
    <h1 class="siteTitle">Forms-R-Us</h1>
    <section class="content">
      <webform
        title="Send a Friend Some Live-Badgers®"
        form-id="badgerForm"
        :fields="badgerFormFields"
        submitText="Badger ’Em!"
        :submitAction="badgerEm"
        icon="bx:shocked"
      />
    </section>
  </div>
</template>

<script>
import Webform from "./components/Webform.vue";
export default {
  name: "App",
  components: { Webform },
  methods: {
    badgerEm() {
      let string = "Your form data! \n";
      this.badgerFormFields.forEach((element) => {
        string += element.variableName + ": " + element.value + "\n";
      });
      alert(string)
      //alert(string);
    },
  },
  data() {
    return {
      badgerFormFields: [
        {
          type: "textInput",
          value: "",
          variableName: "senderName",
          title: "Your Full Name",
          placeholder: "ex. John Doe",
          required: true,
        },
        {
          type: "select",
          value: '',
          variableName: "badgerCount",
          title: "Number of Badgers",
          options: [
            {
              value: 1,
              name: "One",
            },
            {
              value: 2,
              name: "Two",
            },
            {
              value: 3,
              name: "Three",
            },
            {
              value: 4,
              name: "Four",
            },
            {
              value: 5,
              name: "Five",
            },
            {
              value: 6,
              name: "Six",
            },
            {
              value: 7,
              name: "Seven",
            },
            {
              value: 8,
              name: "Eight",
            },
          ],
          required: true,
        },
        {
          type: "radioButtons",
          variableName: "hungriness",
          title: "How Hungry Should the Badgers Be?",
          required: true,
          value: "",
          options: [
            { title: "Ravenous", name: "ravenous" },
            { title: "A Mite Peckish", name: "peckish" },
            { title: "Still Quite Full From Last Meal", name: "full" },
          ],
        },
        {
          type: "checkboxes",
          variableName: "otherShippables",
          title: "What Else Should We Include?",
          required: false,
          value: [],
          options: [
            { title: "Band-Aids", name: "bandaids" },
            { title: "Tylenol", name: "tylenol" },
            { title: "Glitter", name: "glitter" },
          ],
        },
        {
          type: "textInput",
          value: "",
          variableName: "recipientName",
          title: "Victim Full Name",
          placeholder: "ex. James McBadgered",
          required: true,
        },
        {
          type: "textInput",
          value: "",
          variableName: "street1",
          title: "Street",
          placeholder: "ex. 1234 Badger Lane",
          required: true,
        },
        {
          type: "textInput",
          value: "",
          variableName: "street2",
          title: "Street 2",
          placeholder: "ex. Apt. D",
          required: false,
        },
        {
          type: "textInput",
          value: "",
          variableName: "city",
          title: "City",
          placeholder: "ex. New Badger City",
          required: true,
        },
        {
          type: "textInput",
          value: "",
          variableName: "state",
          title: "State",
          placeholder: "ex. Pennsylvania",
          required: true,
        },
        {
          type: "textInput",
          value: "",
          variableName: "zipcode",
          title: "Zip Code",
          placeholder: "ex. 19019",
          required: true,
        },
      ],
    };
  },
};
</script>

<style lang="scss">
@import "~normalize.css";
@import url("https://fonts.googleapis.com/css2?family=Outfit:wght@100;200;500;800&display=swap");
html {
  font-size: 18px;
  body {
    font-family: "outfit", "avenir", sans-serif;
    font-weight: 200;
    font-size: 1em;
    background: #0d3b66;
    box-sizing: border-box;
    color: #222;
    line-height: 1.65;
    * {
      box-sizing: border-box;
    }
    h1.siteTitle {
      text-align: center;
      font-weight: 800;
      font-size: 3em;
      color: #0d3b66;
      background: #f4d35e;
      margin-top: 0;
      padding: 0.25em;
      box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.42);
    }
    section.content {
      display: flex;
      padding: 0 0.5em;
      justify-content: center;
    }
  }
}
</style>
