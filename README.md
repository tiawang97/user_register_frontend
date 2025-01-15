# Registration Form Application

## Overview
This application is a Vue.js-based form designed to collect user information with a focus on usability and validation. The form ensures proper input formatting and guides users through the registration process while maintaining a clean and intuitive design.

## Features
1. **User Information Input**
   - Fields for surname (姓), given name (名), surname in Katakana, and given name in Katakana.
   - Gender selection with three options: 男性 (Male), 女性 (Female), 無回答・その他 (No Answer/Others).
   - Age input field that accepts only positive integers.

2. **Real-Time Validation**
   - Name fields allow only Japanese or English alphabets.
   - Age field restricts input to positive integers and displays an error for invalid entries.
   - Error messages are displayed inline for each field.

3. **Dynamic Button State**
   - The "Register" button is disabled until all fields are correctly filled out and valid.

4. **Error Handling**
   - Displays appropriate error messages if the form is submitted with invalid data.
   - Ensures all required fields are completed before submission.

5. **Navigation**
   - Includes a "Back" button to return to the previous page.

6. **Responsive Design**
   - Mobile-friendly layout with a maximum width of 400px for the form container.

## Technologies Used
- **Vue.js**: Framework for building the form's interactive features.
- **HTML5**: Markup for the form structure.
- **CSS3**: Styling for a responsive and user-friendly interface.

## Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```
2. Navigate to the project directory:
   ```bash
   cd registration-form
   ```
3. Install dependencies:
   ```bash
   npm install
   ```
4. Start the development server:
   ```bash
   npm run serve
   ```

## Usage
1. Open the application in your browser by navigating to `http://localhost:8080` (default port).
2. Fill in all required fields:
   - Enter surname and given name in Japanese or English.
   - Select your gender.
   - Enter your age (positive integers only).
3. If any errors occur, correct them based on the inline error messages.
4. Click the "Register" button to submit the form.
5. Use the "Back" button to return to the previous page if necessary.

## File Structure
- **`App.vue`**: Main component containing the form layout and logic.
- **`styles.css`**: Scoped styles for form appearance.
- **`methods`**:
  - `validateName(field)`: Ensures name fields contain only valid characters.
  - `validateAge()`: Validates the age field for positive integers.
  - `handleRegister()`: Handles form submission.
  - `goBack()`: Navigates to the previous page.

## Customization
- Modify the error messages in the `errors` object within the `data()` function.
- Adjust the form styling by editing the CSS in the `<style scoped>` section.

## License
This project is licensed under the MIT License. Feel free to use and modify it for personal or commercial purposes.

---
Thank you for using this registration form application! If you encounter any issues or have suggestions for improvement, please feel free to contribute or raise an issue in the repository.