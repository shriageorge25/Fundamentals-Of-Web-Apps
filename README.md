# 1. Normal Notes App (non-SPA)

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Types note + clicks Save
    Browser->>Server: POST new note (JSON data)
    Server-->>Browser: "Note saved" response
    Browser->>Server: (maybe) GET all notes again
    Server-->>Browser: List of notes (now includes new one)
    Browser->>User: Shows updated list on the page
```mermaid
sequenceDiagram
    participant Browser
    participant Server

    Browser->>Server: GET /spa
    Server-->>Browser: HTML document
    Browser->>Server: GET /main.css
    Server-->>Browser: CSS file
    Browser->>Server: GET /spa.js
    Server-->>Browser: JS file
    Note right of Browser: Browser runs JS which fetches data.json
    Browser->>Server: GET /data.json
    Server-->>Browser: Notes data
    Note right of Browser: Browser renders notes dynamically
```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Types a note and clicks Save
    Note right of Browser: JS sends the note via fetch (no reload)
    Browser->>Server: POST /new_note_spa with JSON {content, date}
    Server-->>Browser: 201 Created
    Note right of Browser: Browser updates the note list instantly
