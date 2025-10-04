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

