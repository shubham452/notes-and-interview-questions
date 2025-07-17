

---

## ✅ Topics to Know in React Forms

---

### 1. **Controlled vs Uncontrolled Components**

| Feature         | Controlled                               | Uncontrolled               |
| --------------- | ---------------------------------------- | -------------------------- |
| Value source    | React state (`useState`)                 | DOM (`ref`)                |
| Recommended for | Most React forms (predictable)           | Simple/legacy integrations |
| Example         | `<input value={state} onChange={...} />` | `<input ref={myRef} />`    |

---

### 2. **Handling Input Changes**

* Use `onChange` to update form state
* Use one `useState()` per field or a single object for the whole form

```jsx
const [name, setName] = useState('');

<input value={name} onChange={e => setName(e.target.value)} />
```

---

### 3. **Form Submission**

* Use `onSubmit` on `<form>` element
* Prevent default HTML refresh behavior using `e.preventDefault()`

```jsx
<form onSubmit={handleSubmit}>
  <button type="submit">Submit</button>
</form>
```

---

### 4. **Validation Techniques**

* Manual validation with if/else
* HTML5 native validations (`required`, `minLength`, `pattern`)
* Custom validation logic
* Libraries: `yup`, `zod`, `joi`, `validator.js`

---

### 5. **Handling Multiple Fields**

```jsx
const [form, setForm] = useState({ name: '', email: '' });

<input
  name="name"
  value={form.name}
  onChange={e => setForm({ ...form, [e.target.name]: e.target.value })}
/>
```

---

### 6. **Form Libraries**

* **react-hook-form** (minimal, performant)
* **Formik** (more structured, formik bag, schema validation)
* **Final Form** (enterprise-scale projects)

Benefits:

* Less boilerplate
* Built-in validation
* Performance optimizations

---

### 7. **Textarea and Select Handling**

```jsx
<textarea value={message} onChange={e => setMessage(e.target.value)} />

<select value={gender} onChange={e => setGender(e.target.value)}>
  <option value="male">Male</option>
  <option value="female">Female</option>
</select>
```

---

### 8. **File Inputs**

* `input type="file"` can’t be fully controlled
* Use `e.target.files[0]` to access uploaded file
* Can preview file or send via `FormData`

```jsx
<input type="file" onChange={e => setFile(e.target.files[0])} />
```

---

### 9. **Disable Submit Button**

* Disable until required fields are filled or validated

```jsx
<button disabled={!formIsValid}>Submit</button>
```

---

### 10. **Resetting the Form**

* Manual reset by setting state to initial values
* `react-hook-form` provides `reset()` API

---

### 11. **Form Accessibility (a11y)**

* Always associate labels with inputs using `htmlFor`
* Use semantic tags like `<form>`, `<label>`, `<fieldset>`, etc.
* Indicate validation errors clearly for screen readers

---

### 12. **Common Interview Use Cases**

* Build login/signup/contact forms
* Add dynamic fields (e.g., add more education rows)
* Validated forms with error messages
* Integrating file upload + progress
* React Hook Form + Yup validation

---

Would you like:

* These notes added to your document?
* Code examples using `react-hook-form`?
* Interview questions from this topic?
