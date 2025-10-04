```mermaid
##When user opens the app
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



## When user opens the SPA version
sequenceDiagram
    participant Browser
    participant Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate Server
    Server-->>Browser: HTML document
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate Server
    Server-->>Browser: CSS file
    deactivate Server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate Server
    Server-->>Browser: JavaScript file
    deactivate Server

    Note right of Browser: Browser runs spa.js which fetches the notes data from server

    Browser->>Server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate Server
    Server-->>Browser: JSON data of existing notes
    deactivate Server

    Note right of Browser: Browser renders notes dynamically without reloading the page

## When user creates a new note in the SPA version
sequenceDiagram
    participant User
    participant Browser
    participant Server

    User->>Browser: Types a note and clicks Save
    Note right of Browser: JavaScript captures the input (no page reload)
    Browser->>Server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa<br>with JSON data { content, date }
    activate Server
    Server-->>Browser: 201 Created (confirmation)
    deactivate Server
    Note right of Browser: Browser updates the notes list on the page using JS<br>without reloading

