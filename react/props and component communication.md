**✅ 1. Props Drilling**

**Definition:** Passing data through multiple layers of components.

jsx

Copy code

const Parent = () =&gt; &lt;Child name="Alice" /&gt;;

const Child = ({ name }) =&gt; &lt;GrandChild name={name} /&gt;;

const GrandChild = ({ name }) =&gt; &lt;p&gt;{name}&lt;/p&gt;;

🔍 **Problem:** Deep chains make code harder to manage.

✅ **Solutions:** Context API or state management libraries (e.g.,
Redux).

**🔄 2. Callback Functions as Props**

Used to **communicate from child → parent**.

jsx

Copy code

const Parent = () =&gt; {

const handleClick = (value) =&gt; console.log(value);

return &lt;Child onClick={handleClick} /&gt;;

};

const Child = ({ onClick }) =&gt; (

&lt;button onClick={() =&gt; onClick("Hi!")}&gt;Click&lt;/button&gt;

);

**👶 3. Children & props.children**

Pass JSX elements or components as children.

jsx

Copy code

const Wrapper = ({ children }) =&gt; (

&lt;div className="box"&gt;{children}&lt;/div&gt;

);

// Usage

&lt;Wrapper&gt;

&lt;p&gt;Hello from inside!&lt;/p&gt;

&lt;/Wrapper&gt;

**⚖️ 4. Composition vs Inheritance**

  **Concept**       **Description**                           **Preferred in React**
  ----------------- ----------------------------------------- ------------------------
  **Composition**   Build components using other components   ✅ Yes
  Inheritance       Extend classes from base components       🚫 No (not recommended)

jsx

Copy code

// Composition

const Card = ({ header, content }) =&gt; (

&lt;div&gt;

{header}

{content}

&lt;/div&gt;

);

**🛠️ 5. Default Props & PropTypes**

**Default Props**

jsx

Copy code

const Button = ({ label = "Click me" }) =&gt;
&lt;button&gt;{label}&lt;/button&gt;;

Or with static property:

jsx

Copy code

Button.defaultProps = { label: "Click me" };

**PropTypes (Runtime validation)**

jsx

Copy code

import PropTypes from 'prop-types';

Button.propTypes = {

label: PropTypes.string.isRequired,

onClick: PropTypes.func,

};
