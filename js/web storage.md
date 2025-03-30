**1. Web Storage (localStorage, sessionStorage, cookies)**

  ----------------------------------------------------------------------------
  **Feature**        **Scope**         **Expiry**               **Capacity**
  ------------------ ----------------- ------------------------ --------------
  localStorage       Browser-wide      Never expires            \~5MB

  sessionStorage     Per tab/session   Expires on tab close     \~5MB

  Cookies            Domain-specific   Set manually, or expires \~4KB
  ----------------------------------------------------------------------------

**Examples:**

// localStorage

localStorage.setItem(\"username\", \"John\");

console.log(localStorage.getItem(\"username\")); // \"John\"

localStorage.removeItem(\"username\");

// sessionStorage

sessionStorage.setItem(\"sessionID\", \"abc123\");

console.log(sessionStorage.getItem(\"sessionID\")); // \"abc123\"

sessionStorage.clear();

// Cookies

document.cookie = \"token=xyz; expires=Fri, 31 Dec 9999 23:59:59 GMT;
path=/\";

console.log(document.cookie); // \"token=xyz\"
