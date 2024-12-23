
# User Management Screen Specification

## **Overview**
The User Management Screen is a UI for managing user accounts, enabling administrators to create, update, or view user information. This specification outlines all UI components, their behaviors, and interactions.

---

## **Initial View**
When the page is loaded, the following components will be displayed:
1. **User List Table**: Displays existing users with their details.
   - Columns: 
     - ID
     - Username
     - Email
     - Enabled (true/false)
2. **"New User" Form**: A collapsible/hidden section to add a new user.
3. **Toolbar**:
   - "+ New User" button: Opens the form to create a new user.
   - "Hide Disabled Users" checkbox: Filters out disabled users from the table when checked.
   - "Save User" button: Saves user details after creation or update.

---

## **UI Components**

### **1. User List Table**
- **Columns**:
  - `ID`: Displays the user's unique identifier.
  - `User Name`: Shows the username of the user.
  - `Email`: Displays the user's email address.
  - `Enabled`: A boolean value indicating if the user account is active.

- **Features**:
  - **Sorting**: Each column header has a sorting feature to sort data in ascending/descending order.
  - **Row Selection**: Selecting a row pre-fills the "New User" form with user details for editing.

---

### **2. Toolbar**
- **"+ New User" Button**:
  - Action: Clears the "New User" form and opens it for adding a new user.
  - Behavior: Scrolls or expands the form section if it is hidden.

- **"Hide Disabled Users" Checkbox**:
  - Action: Filters the table to hide rows where the `Enabled` value is `false`.
  - Behavior: Toggles between showing all users and hiding disabled users.

- **"Save User" Button**:
  - Action: Validates the form fields and submits user data to the backend API.
  - Behavior: 
    - **Success**: Shows a confirmation message (e.g., "User saved successfully").
    - **Failure**: Displays an error message if validation fails or the server responds with an error.

---

### **3. New User Form**
- **Fields**:
  - **Username** (Text Input): Mandatory field to input the username.
  - **Display Name** (Text Input): Optional field for the user’s display name.
  - **Phone** (Text Input): Optional field for the user's phone number.
  - **Email** (Text Input): Mandatory field for the user's email.
  - **User Roles** (Dropdown): Allows the selection of one or more roles from the following options:
    - Guest
    - Admin
    - SuperAdmin
  - **Enabled** (Checkbox): Toggles the enabled status of the user (checked = true, unchecked = false).

- **Behavior**:
  - Fields are editable and support tab navigation.
  - "Save User" updates the user table with new or modified details.

---

## **Behavior Details**
1. **At Page Load**:
   - All existing users are displayed in the table.
   - The "New User" form is collapsed or hidden by default.
   - The "Hide Disabled Users" checkbox is unchecked, displaying all users.

2. **Filter Users**:
   - When the "Hide Disabled Users" checkbox is checked, rows where `Enabled = false` are hidden.
   - When unchecked, all users are displayed.

3. **Adding a New User**:
   - Clicking "+ New User" clears the form and allows for input.
   - On clicking "Save User":
     - If all mandatory fields are filled and valid, the user is added to the table.
     - If validation fails, an error message is displayed next to the relevant field.

4. **Editing an Existing User**:
   - Clicking a row in the table pre-fills the form with that user's data.
   - Modifying and saving updates the existing user's data.

5. **Form Validation**:
   - Fields like `Username` and `Email` are required.
   - Invalid inputs (e.g., invalid email format) will prevent form submission, showing an error message.

---

## **API Integration**
- **Endpoints**:
  - **GET /users**: Fetch all user details to populate the table.
  - **POST /users**: Add a new user.
  - **PUT /users/{id}**: Update user details.
  - **DELETE /users/{id}**: Delete a user.

---

## **Styling**
- Consistent with the application’s design system.
- Responsive layout for desktop and mobile views.

---

## **Error Handling**
- Display a user-friendly error message for the following scenarios:
  - Invalid form inputs.
  - Failed server requests.
  - Attempt to save duplicate usernames or emails.
