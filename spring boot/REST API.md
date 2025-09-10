Here are notes with coding examples used in the provided YouTube transcript:

### Project Setup and Basic Concepts

1.  **Project Initialization**:
    *   A new Spring Boot project is created using **Spring Initializr**.
    *   **Java** and **Maven** are selected.
    *   **Spring Boot version 2.7.16** is chosen for better support and resources.
    *   **Group ID**: `e.digest.engineering.digest` (represents the company name in reverse domain fashion).
    *   **Artifact ID**: `journal-app` (represents a unique project within the company, lower-case start is recommended).
    *   **Name**: `Journal App` (human-readable name).
    *   **Description**: `End-to-End Encrypted Journal App`.
    *   **Dependency**: `Spring Web` is added for creating REST APIs.

2.  **Main Application Class Renaming**:
    *   The automatically generated `JournalAppApplication` class is **refactored** (renamed globally) to `JournalApplication`.
    *   *Coding Example:*
        ```java
        // Original (example, not in source directly but implied)
        public class JournalAppApplication { /* ... */ }

        // Renamed to
        public class JournalApplication { /* ... */ }
        ```

3.  **REST API Definition**:
    *   **REST API** stands for **Representational State Transfer Application Programming Interface**.
    *   It is defined as **HTTP Verb + URL**.
    *   **HTTP Verbs** (methods) indicate the action to be performed:
        *   **GET**: To retrieve or view data.
        *   **POST**: To create new data.
        *   **PUT**: To modify or update existing data.
        *   **DELETE**: To remove data.
    *   **Representation State Transfer** means that the client and server understand each other's representation and transfer information (state) between them.

### Controller for Handling HTTP Requests

1.  **Controller Package and Class**:
    *   A new package named `journal-app.controller` is created.
    *   Inside this package, a new Java class named `JournalEntryController` is created.
    *   *Coding Example (Conceptual):*
        ```
        src
        └── main
            └── java
                └── com
                    └── e
                        └── digest
                            └── engineering
                                └── digest
                                    └── journalapp
                                        ├── JournalApplication.java
                                        ├── controller
                                        │   └── JournalEntryController.java
                                        └── entity
                                            └── JournalEntry.java
        ```

2.  **`@RestController` Annotation**:
    *   The `JournalEntryController` class is annotated with `@RestController`.
    *   This annotation marks the class as a special type of **Spring Component** (making it a Bean in the IoC container) that can handle HTTP requests and automatically convert return values to JSON (or XML).
    *   *Coding Example:*
        ```java
        package com.e.digest.engineering.digest.journalapp.controller;

        import org.springframework.web.bind.annotation.RestController;

        @RestController
        public class JournalEntryController {
            // ... API endpoints
        }
        ```

3.  **Class-Level `@RequestMapping`**:
    *   To define a base path for all endpoints within a controller, `@RequestMapping` can be used at the class level.
    *   *Coding Example:*
        ```java
        package com.e.digest.engineering.digest.journalapp.controller;

        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RestController;

        @RestController
        @RequestMapping("journal") // All methods in this controller will have "/journal" as a prefix
        public class JournalEntryController {
            // ... endpoints like /journal/health-check, /journal, /journal/{id}
        }
        ```

### API Endpoints (RESTful Services)

1.  **Health Check Endpoint (GET)**:
    *   This endpoint is created to verify if the application is running.
    *   It uses `@GetMapping` with a specific path.
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import org.springframework.web.bind.annotation.GetMapping;

        // ...
        @GetMapping("health-check")
        public String healthCheck() {
            return "OK"; // Returns "OK" as a String, automatically converted if JSON is expected.
        }
        ```
    *   **Example Usage**: A GET request to `http://localhost:8080/journal/health-check` (if `@RequestMapping("journal")` is present) or `http://localhost:8080/health-check` (if no class-level mapping) would return `"OK"`.

### Data Model (POJO)

1.  **Entity Package and Class**:
    *   A new package named `journal-app.entity` is created.
    *   Inside this package, a new Java class named `JournalEntry` is created.
    *   This class represents the structure of a journal entry, also known as a **Plain Old Java Object (POJO)**.
    *   *Coding Example:*
        ```java
        package com.e.digest.engineering.digest.journalapp.entity;

        public class JournalEntry {
            private Long id;
            private String title;
            private String content;

            // Getters and Setters for all fields are generated
            public Long getId() { return id; }
            public void setId(Long id) { this.id = id; }
            public String getTitle() { return title; }
            public void setTitle(String title) { this.title = title; }
            public String getContent() { return content; }
            public void setContent(String content) { this.content = content; }
        }
        ```

### In-Memory Data Storage (Temporary)

1.  **`Map` for Journal Entries**:
    *   Since no database is used in this video, a `HashMap` is used as an in-memory data store to simulate a database table.
    *   The `Map` uses `Long` as the key (for the `id` of the journal entry) and `JournalEntry` objects as values.
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import java.util.HashMap;
        import java.util.Map;
        import com.e.digest.engineering.digest.journalapp.entity.JournalEntry;

        // ...
        private Map<Long, JournalEntry> journalEntries = new HashMap<>();
        ```

### CRUD Operations (Create, Read, Update, Delete)

1.  **Get All Journal Entries (GET)**:
    *   This endpoint retrieves all journal entries from the in-memory `Map`.
    *   `@GetMapping` is used without a specific path, meaning it maps to the class-level `@RequestMapping` path (`/journal`).
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import java.util.ArrayList;
        import java.util.List;
        import org.springframework.web.bind.annotation.GetMapping;

        // ...
        @GetMapping // Maps to /journal (if class-level @RequestMapping is "journal")
        public List<JournalEntry> getAll() {
            return new ArrayList<>(journalEntries.values()); // Returns all entries as a list
        }
        ```
    *   **Example Usage**: A GET request to `http://localhost:8080/journal` would return a JSON array of all journal entries.

2.  **Create Journal Entry (POST)**:
    *   This endpoint creates a new journal entry.
    *   `@PostMapping` is used, also mapping to the class-level path (`/journal`).
    *   The `@RequestBody` annotation is used to receive the `JournalEntry` object as JSON in the request body.
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import org.springframework.web.bind.annotation.PostMapping;
        import org.springframework.web.bind.annotation.RequestBody;

        // ...
        @PostMapping // Maps to /journal (if class-level @RequestMapping is "journal")
        public Boolean createEntry(@RequestBody JournalEntry myEntry) {
            journalEntries.put(myEntry.getId(), myEntry); // Adds the new entry to the map
            return true; // Returns true on successful creation
        }
        ```
    *   **Example Usage**: A POST request to `http://localhost:8080/journal` with a JSON body like `{"id": 1, "title": "Morning", "content": "Morning was good"}` would create a new entry.

3.  **Get Journal Entry by ID (GET)**:
    *   This endpoint retrieves a specific journal entry by its ID.
    *   `@GetMapping("{myId}")` is used to define a path that includes a **path variable** (`myId`).
    *   The `@PathVariable` annotation extracts the `myId` from the URL path and binds it to a method parameter.
    *   *Path Variable vs. Request Parameter*:
        *   **Path Variable**: `http://localhost:8080/journal/2` (`2` is the path variable).
        *   **Request Parameter**: `http://localhost:8080/journal?name=vipul` (`name=vipul` is the request parameter).
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import org.springframework.web.bind.annotation.PathVariable;

        // ...
        @GetMapping("{myId}") // Maps to /journal/{myId}
        public JournalEntry getJournalEntryById(@PathVariable("myId") Long myId) {
            return journalEntries.get(myId); // Retrieves entry by ID from the map
        }
        ```
    *   **Example Usage**: A GET request to `http://localhost:8080/journal/2` would retrieve the journal entry with ID 2.

4.  **Delete Journal Entry by ID (DELETE)**:
    *   This endpoint deletes a specific journal entry by its ID.
    *   `@DeleteMapping("{myId}")` is used, similar to `GET by ID`, but with the DELETE HTTP verb. This prevents conflicts with other endpoints that might have a similar path but a different verb.
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import org.springframework.web.bind.annotation.DeleteMapping;

        // ...
        @DeleteMapping("{myId}") // Maps to /journal/{myId}
        public Boolean deleteEntryById(@PathVariable("myId") Long myId) {
            return journalEntries.remove(myId) != null; // Removes entry by ID and returns true if removed
        }
        ```
    *   **Example Usage**: A DELETE request to `http://localhost:8080/journal/2` would delete the journal entry with ID 2.

5.  **Update Journal Entry by ID (PUT)**:
    *   This endpoint updates an existing journal entry.
    *   `@PutMapping("{id}")` is used, taking both a path variable (`id`) to identify the entry to update and a `@RequestBody` for the new data.
    *   *Coding Example:*
        ```java
        // Inside JournalEntryController
        import org.springframework.web.bind.annotation.PutMapping;

        // ...
        @PutMapping("{id}") // Maps to /journal/{id}
        public JournalEntry updateJournalById(@PathVariable("id") Long id, @RequestBody JournalEntry myEntry) {
            journalEntries.put(id, myEntry); // Overwrites the existing entry with the given ID
            return myEntry; // Returns the updated entry
        }
        ```
    *   **Example Usage**: A PUT request to `http://localhost:8080/journal/2` with a JSON body like `{"id": 2, "title": "Evening", "content": "Evening was calm"}` would update the journal entry with ID 2.
