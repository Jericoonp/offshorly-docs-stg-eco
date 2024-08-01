# Registration Form in ReactJS

This documentation provides a simple example of a registration form implemented in ReactJS using JavaScript. The form includes fields for username, email, password, and password confirmation, along with basic validation and submission handling.

## Component Structure

```jsx
import React, { useState } from 'react';

const RegistrationForm = () => {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: '',
    confirmPassword: '',
  });
  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (validateForm()) {
      console.log('Form submitted:', formData);
      // Add your form submission logic here
    }
  };

  const validateForm = () => {
    let isValid = true;
    const newErrors = {};

    if (!formData.username.trim()) {
      newErrors.username = 'Username is required';
      isValid = false;
    }

    if (!formData.email.trim()) {
      newErrors.email = 'Email is required';
      isValid = false;
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      newErrors.email = 'Email is invalid';
      isValid = false;
    }

    if (!formData.password) {
      newErrors.password = 'Password is required';
      isValid = false;
    } else if (formData.password.length < 6) {
      newErrors.password = 'Password must be at least 6 characters';
      isValid = false;
    }

    if (formData.password !== formData.confirmPassword) {
      newErrors.confirmPassword = 'Passwords do not match';
      isValid = false;
    }

    setErrors(newErrors);
    return isValid;
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="username">Username:</label>
        <input
          type="text"
          id="username"
          name="username"
          value={formData.username}
          onChange={handleChange}
        />
        {errors.username && <span className="error">{errors.username}</span>}
      </div>
      <div>
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
        {errors.email && <span className="error">{errors.email}</span>}
      </div>
      <div>
        <label htmlFor="password">Password:</label>
        <input
          type="password"
          id="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
        />
        {errors.password && <span className="error">{errors.password}</span>}
      </div>
      <div>
        <label htmlFor="confirmPassword">Confirm Password:</label>
        <input
          type="password"
          id="confirmPassword"
          name="confirmPassword"
          value={formData.confirmPassword}
          onChange={handleChange}
        />
        {errors.confirmPassword && (
          <span className="error">{errors.confirmPassword}</span>
        )}
      </div>
      <button type="submit">Register</button>
    </form>
  );
};

export default RegistrationForm;
```

## Usage

To use this registration form component in your React application, follow these steps:

1. Create a new file named `RegistrationForm.js` and paste the above code into it.
2. Import and use the component in your main application file or any other component:

```jsx
import React from 'react';
import RegistrationForm from './RegistrationForm';

const App = () => {
  return (
    <div>
      <h1>Registration</h1>
      <RegistrationForm />
    </div>
  );
};

export default App;
```

## Explanation

- The component uses the `useState` hook to manage form data and error states.
- `handleChange` function updates the form data as the user types.
- `handleSubmit` function prevents the default form submission, validates the form, and logs the form data if valid.
- `validateForm` function checks for empty fields, valid email format, password length, and password match.
- The form renders input fields for username, email, password, and password confirmation.
- Error messages are displayed below each input field when validation fails.

## Styling

To add basic styling to your form, you can create a CSS file (e.g., `RegistrationForm.css`) and import it in your component:

```css
form {
  max-width: 300px;
  margin: 0 auto;
}

div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 5px;
}

.error {
  color: red;
  font-size: 0.8em;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 15px;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
```

Import the CSS file in your `RegistrationForm.js`:

```jsx
import React, { useState } from 'react';
import './RegistrationForm.css';

// ... rest of the component code
```

This example provides a basic structure for a registration form in ReactJS. You can further customize the component by adding more fields, implementing more complex validation, or integrating it with a backend API for actual user registration.
