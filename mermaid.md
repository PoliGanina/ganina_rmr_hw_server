```mermaid
sequenceDiagram
    %%https://mermaid-js.github.io/mermaid/#/sequenceDiagram
    actor User
    participant client
    participant server
    participant DB

    User->>client: types email/tel & password 

    alt Client-side validation
        client->>User: result of validation
    else failed
        client->>User: error label with validation rules
    else success
        client->>User: style form like OK (enable Login button)
    end

    User->>client: submit login

    alt Server-side validation
        client->>server: POST data to DB
        server->>DB: request data 
        DB->>server: JSON
        server->>server: validation
    else failed
        server->>client: status 401
        client->>User: "access denied :-(" / "incorrect password"
    else success
        server->>client: status 200, cookies & picture of cat
        client->>User: render cat.jpg
    end

```
