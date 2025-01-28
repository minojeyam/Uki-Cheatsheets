# HTML Forms Worksheet

HTML forms are essential for collecting user input on websites. This worksheet explores all the common input types, attributes, and elements used in forms. A sample form code is included for hands-on practice.

---

## **Form Elements and Descriptions**

### **1. `<form>`**
The `<form>` element defines an HTML form for user input. Attributes:
- `action`: URL where the form data is sent after submission.
- `method`: HTTP method (`GET` or `POST`) used when sending data.
- `enctype`: Specifies how the form data is encoded (`application/x-www-form-urlencoded`, `multipart/form-data`, or `text/plain`).

### **2. `<input>`**
The `<input>` element defines a variety of input fields. It has several types:

#### Text Fields
- `type="text"`: Single-line text input.
- `type="password"`: Masks input for sensitive information.
- `type="email"`: Input for email addresses (validates email format).
- `type="number"`: Input for numerical values with options like `min`, `max`, and `step`.
- `type="tel"`: Input for telephone numbers.

#### Selection and Options
- `type="radio"`: Select one option from multiple choices.
  - **Attributes:**
    - `id`: Associates the radio button with its label.
    - `name`: Groups related radio buttons so only one can be selected at a time.
    - `value`: Represents the data sent when the button is selected.
- `type="checkbox"`: Select multiple options.
  - **Attributes:**
    - `id`: Associates the checkbox with its label.
    - `name`: Groups related checkboxes for multiple selections.
    - `value`: Represents the data sent when the checkbox is checked.

#### Buttons
- `type="submit"`: Submit the form.
- `type="reset"`: Reset the form fields to their initial values.
- `type="button"`: A generic button (requires JavaScript to perform an action).

#### Specialized Inputs
- `type="date"`: Input for selecting a date.
- `type="color"`: Input for selecting a color.
- `type="file"`: Input for file uploads.
- `type="hidden"`: Stores hidden data sent with the form.
- `type="range"`: Input for selecting a value within a range (slider).
- `type="search"`: Input for search fields.
- `type="url"`: Input for website URLs.

### **3. `<label>`**
The `<label>` element describes each input field and associates it using the `for` attribute, which matches the `id` of the input.

### **4. `<select>` and `<option>`**
Dropdown menu for selecting options. Each option is enclosed in `<option>` tags.
  - **Attributes:**
    - `id`: Associates the dropdown with its label.
    - `name`: Identifies the field name for data submission.

### **5. `<textarea>`**
For multi-line text input.

---

## **Sample Form Code**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML Forms Worksheet</title>
</head>
<body>
    <h1>Sample HTML Form</h1>
    <form action="/submit" method="POST">
        <!-- Text Input -->
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" placeholder="Enter your username" required><br><br>

        <!-- Password Input -->
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br><br>

        <!-- Email Input -->
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" placeholder="example@example.com" required><br><br>

        <!-- Date Input -->
        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" name="dob"><br><br>

        <!-- Dropdown -->
        <label for="country">Country:</label>
        <select id="country" name="country">
            <option value="">Select your country</option>
            <option value="us">United States</option>
            <option value="uk">United Kingdom</option>
            <option value="ca">Canada</option>
        </select><br><br>

        <!-- Radio Buttons -->
        <label>Gender:</label><br>
        <input type="radio" id="male" name="gender" value="male">
        <label for="male">Male</label><br>
        <input type="radio" id="female" name="gender" value="female">
        <label for="female">Female</label><br><br>

        <!-- Checkboxes -->
        <label>Hobbies:</label><br>
        <input type="checkbox" id="sports" name="hobbies" value="sports">
        <label for="sports">Sports</label><br>
        <input type="checkbox" id="music" name="hobbies" value="music">
        <label for="music">Music</label><br>
        <input type="checkbox" id="travel" name="hobbies" value="travel">
        <label for="travel">Travel</label><br><br>

        <!-- File Input -->
        <label for="profile-pic">Upload Profile Picture:</label>
        <input type="file" id="profile-pic" name="profile-pic"><br><br>

        <!-- Submit and Reset Buttons -->
        <button type="submit">Submit</button>
        <button type="reset">Reset</button>
    </form>
</body>
</html>
```

---

### **Exercises**

1. Add a `tel` input for phone numbers in the sample form.
2. Include a `range` slider for selecting an age group.
3. Add validation to ensure the email input contains a valid email address.
4. Create a new form for a feedback page using at least three input types.

---

### **Difference Between `id` and `name`**

#### **`id`**
- **Purpose**: Uniquely identifies an element in the HTML document.
- **Use Case**: Typically used for associating labels (`<label>`), applying CSS styles, or targeting elements with JavaScript.
- **Uniqueness**: Must be unique within the entire document.
- **Example**:
  ```html
  <input type="text" id="username" name="username">
  <label for="username">Username</label>
  ```
  - The `label` is linked to the input using the `id="username"`.

#### **`name`**
- **Purpose**: Specifies the name of the input field for data submission.
- **Use Case**: Used by the browser to group form values when sending data to the server.
- **Uniqueness**: Can be shared among multiple elements (e.g., radio buttons or checkboxes) when they belong to the same group.
- **Example**:
  ```html
  <input type="radio" id="male" name="gender" value="male">
  <input type="radio" id="female" name="gender" value="female">
  ```
  - The `name="gender"` groups the two radio buttons so only one can be selected.

#### Summary:
| Attribute | Purpose                              | Must Be Unique? | Used For                           |
|-----------|--------------------------------------|-----------------|-------------------------------------|
| `id`      | Unique identifier for an element.   | Yes             | Labels, CSS, and JavaScript.       |
| `name`    | Groups data for form submission.    | No              | Sending grouped input to the server. |

#### Specialized Inputs Form

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Specialized Inputs Form</title>
</head>
<body>
    <h1>Specialized Inputs Form</h1>
    <form action="/submit-specialized" method="POST" enctype="multipart/form-data">

        <!-- Color Picker -->
        <label for="fav-color">Favorite Color:</label>
        <input type="color" id="fav-color" name="fav-color"><br><br>

        <!-- Range Slider -->
        <label for="satisfaction">Satisfaction Level (1-10):</label>
        <input type="range" id="satisfaction" name="satisfaction" min="1" max="10" value="5"><br><br>

        <!-- File Upload -->
        <label for="resume">Upload Your Resume:</label>
        <input type="file" id="resume" name="resume" accept=".pdf,.doc,.docx"><br><br>

        <!-- Date-Time Local -->
        <label for="appointment">Choose an Appointment Time:</label>
        <input type="datetime-local" id="appointment" name="appointment"><br><br>

        <!-- Month Selector -->
        <label for="birth-month">Birth Month:</label>
        <input type="month" id="birth-month" name="birth-month"><br><br>

        <!-- Week Selector -->
        <label for="work-week">Preferred Work Week:</label>
        <input type="week" id="work-week" name="work-week"><br><br>

        <!-- Hidden Input -->
        <input type="hidden" id="user-id" name="user-id" value="12345">

        <!-- Submit Button -->
        <button type="submit">Submit</button>
    </form>
</body>
</html>
