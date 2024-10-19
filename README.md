# Backend Server for Blog Application

This README provides an overview of the backend server for a blog application. The server is built using Rust and utilizes SQLite as its database.

## Table of Contents

1. [Project Structure](#project-structure)
2. [Data Models](#data-models)
3. [Database Schema](#database-schema)
4. [Environment Configuration](#environment-configuration)
5. [API Responses](#api-responses)
6. [Setup and Installation](#setup-and-installation)
7. [Running the Server](#running-the-server)

## Project Structure

The backend server is structured around a blog application with posts, comments, and users. It uses SQLx for database operations and includes serialization/deserialization support through Serde.

## Data Models
The server uses the following main data models:

### Post

```rust
pub struct Post {
    pub post_id: Option<i64>,
    pub user_id: Option<i64>,
    pub title: String,
    pub markdown: String,
    pub created_at: Option<NaiveDateTime>,
    pub updated_at: Option<NaiveDateTime>,
}
```

### Comment

```rust
pub struct Comment {
    pub comment_id: Option<i64>,
    pub post_id: i64,
    pub user_id: i64,
    pub content: String,
    pub created_at: Option<NaiveDateTime>,
}
```

### User

```rust
pub struct User {
    pub user_id: Option<i64>,
    pub username: String,
    pub email: String,
    pub password: String,
    pub created_at: Option<NaiveDateTime>,
}
```

## Database Schema

The database schema includes three main tables:

1. `post`: Stores blog post information
2. `comment`: Stores comments associated with posts
3. `user`: Stores user information

Foreign key constraints are enforced to maintain data integrity between tables.

## Environment Configuration

The server requires a `.env` file in the root directory with the following variables:

```
DB_URL=db/stp.sqlite
CORS_URL=localhost:3000
PORT=8080
STP_SECRET=SECRETS!
```

Ensure this file is present and correctly configured before running the server otherwise the program will fail at runtime.

## API Responses

The server provides the following response structures:

### PostResponse

```rust
pub struct PostResponse {
    pub post_id: i64,
    pub user_id: i64,
    pub title: String,
    pub markdown: String,
    pub created_at: NaiveDateTime,
    pub updated_at: NaiveDateTime,
    pub author: String,
    pub comments: Vec<CommentResponse>
}
```

### CommentResponse

```rust
pub struct CommentResponse {
    pub comment_id: i64,
    pub post_id: i64,
    pub user_id: i64,
    pub content: String,
    pub created_at: NaiveDateTime,
    pub author: String
}
```

### UserResponse

```rust
pub struct UserResponse {
    pub user_id: i64,
    pub username: String,
    pub created_at: NaiveDateTime
}
```

### TokenResponse

```rust
pub struct TokenResponse {
    pub user: UserResponse,
    pub token: String
}
```

## Setup and Installation

1. Ensure you have Rust and Cargo installed on your system.
2. Clone the repository to your local machine.
3. Navigate to the project directory.
4. Create a `.env` file in the root directory and add the required environment variables as mentioned in the [Environment Configuration](#environment-configuration) section.
5. Run `cargo build` to compile the project and download dependencies.

## Running the Server

To start the server, run the following command in the project root directory:

```
cargo run
```

The server will start and listen on the port specified in the `.env` file (default is 8080).

There is also the files `run.sh` and `run_watch.sh` that are a shortcut for this command.

---

For more detailed information about the API endpoints and usage, please refer to the API documentation (if available) or contact the project maintainers.";