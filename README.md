# Vue.js-Semantic-Form-Validator
This package let's you leverage the **HTML5**'s already awesome form validation capabilities. You get to define your validation rules like you would in a normal HTML form while maintaining full control of how and when your errors are displayed.

## Installation

```
npm install --save vue-semantic-form-validator
```

## Usage

1. Once you've imported the component you can use it in your vue.js template by adding the following:
   - An ```id``` prop to uniquely identify the form.
   - A ```@submit``` event listener which is triggered when there are no invalid input fields in the form.
   - An ```@error``` event listener triggered when there are invalid fields in the form.

2. Inside your form you will need to define two templates. One for the form fields and another for the submit button.
3. In your fields template you can define all your input fields and their validation rules like you would in normal **HTML**. However you can override the default error messages by defining a **title** attribute on the form field.


### Sample Usage

``` html
  <v-form id="v-form" @submit="submitFunction()" @error="errorFunction">
    <template v-slot:fields="vForm">
      <input type="text" required name="name" v-model="book.name" />

      <input type="text" required name="author" v-model="book.author" title="Please fill out the author" />
      <br />
      <small>{{ vForm.errors.name }}</small>
    </template>
    <template v-slot:submit>
      <button>Submit</button>
    </template>
  </v-form>
```

``` js
import vForm from "vue-semantic-form-validator";

export default {
  components: { vForm },
  data: () => ({ book: { name: null, author: null } }),
  methods: {
    errorFunction(errors) {
      console.log(errors);
    },
    submitFunction() {
      console.log(this.book);
      // do anything you want here
    }
  }
};
```

## Tips
You can leverage HTML5 patterns to give even more flexibility on validation rules checkout http://html5pattern.com/ for some cool REGEX patterns developed by the community to solve common problems. I will continue to update this page with some of the creative ways I have used this component.