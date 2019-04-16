# validate.js
Validate.js provides a declarative way of validating javascript objects.
It helps you to validate your HTML inputs by passing an object array of validation parameters.
Include the validation.js file at the bottom of your body tag in you html(e.g. <script type="text/javascript" src="validation.js"></script>)
To validate any input you need to select that input object using selectors API (for e.g. x = document.getElementById('IdName') and pass it to the validation function as a parameter ( e.g. validation(x)).
Then you need to call the valildate method and pass an object array of validation parameters to validate it. (e.g. validation(x).validate([{type:"required"}])
You can also perform multiple validations at once by passing multiple parameters.
Suppose your input field cannot be empty and you also want it to match a certain regex pattern, then you can pass both the parameter as an array to the validate method.
Eg: validation(x).validate([{type:required}, {type:"regex", pattern:"/^\d{1,2}:\d{2}([ap]m)?$/"}])
