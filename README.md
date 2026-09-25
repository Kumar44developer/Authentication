# Authentication App

A full-stack user authentication system built with Node.js, Express, PostgreSQL, and EJS. Users can register with an email and password, log in with their credentials, and access a protected secrets page. Passwords are securely hashed using bcrypt.

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** PostgreSQL
- **Templating Engine:** EJS
- **Password Hashing:** bcrypt
- **Frontend:** Bootstrap 4, Font Awesome 5

## Prerequisites

- [Node.js](https://nodejs.org/) v16 or higher
- [PostgreSQL](https://www.postgresql.org/) v12 or higher
- npm (comes with Node.js)

## Project Structure

```
Authentication/
├── public/
│   └── css/
│       └── styles.css
├── views/
│   ├── partials/
│   │   ├── header.ejs
│   │   └── footer.ejs
│   ├── home.ejs
│   ├── login.ejs
│   ├── register.ejs
│   └── secrets.ejs
├── .env
├── .env.example
├── .gitignore
├── index.js
├── package.json
└── queries.sql
```

## Database Setup

1. Open your PostgreSQL shell or pgAdmin.

2. Create the database:

```sql
CREATE DATABASE secrets;
```

3. Connect to the database and create the users table:

```sql
\c secrets

CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  email VARCHAR(100) NOT NULL UNIQUE,
  password VARCHAR(100)
);
```

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Kumar44developer/Authentication.git
cd Authentication
```

2. Install dependencies:

```bash
npm install
```

3. Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

4. Open `.env` and update the values with your PostgreSQL credentials:

```
DB_USER=postgres
DB_HOST=localhost
DB_NAME=secrets
DB_PASSWORD=your_password_here
DB_PORT=5432
PORT=3000
```

## Running the App

Start the server:

```bash
npm start
```

Start the server in development mode with auto-reload:

```bash
npm run dev
```

The app will be running at `http://localhost:3000`.

## Usage

1. Open `http://localhost:3000` in your browser.
2. Click **Register** to create a new account with your email and password.
3. After registering, you will be redirected to the secrets page.
4. Click **Login** to sign in with your registered email and password.
5. Successful login redirects you to the secrets page.

## API Routes

| Method | Route       | Description                          |
|--------|-------------|--------------------------------------|
| GET    | `/`         | Home page with Register/Login links  |
| GET    | `/login`    | Login form                           |
| GET    | `/register` | Registration form                    |
| POST   | `/login`    | Authenticates user credentials       |
| POST   | `/register` | Creates a new user account           |

## Environment Variables

| Variable      | Description                | Default     |
|---------------|----------------------------|-------------|
| `DB_USER`     | PostgreSQL username        | `postgres`  |
| `DB_HOST`     | PostgreSQL host            | `localhost` |
| `DB_NAME`     | PostgreSQL database name   | `secrets`   |
| `DB_PASSWORD` | PostgreSQL password        | -           |
| `DB_PORT`     | PostgreSQL port            | `5432`      |
| `PORT`        | Express server port        | `3000`      |

## Bugs Fixed from Original

- **login.ejs** was incomplete with missing password field, submit button, and closing HTML tags
- **register.ejs** was missing the email input field and included `header.ejs` instead of `footer.ejs` at the bottom
- **footer.ejs** was empty with no closing `</body>` and `</html>` tags
- **header.ejs** had a relative CSS path (`css/styles.css`) that broke on nested routes, changed to absolute (`/css/styles.css`)
- **index.js** served static files from a `public/` directory that did not exist, created the proper `public/css/` folder structure
- **index.js** stored passwords in plain text, added bcrypt hashing for registration and bcrypt comparison for login
- **index.js** had hardcoded database credentials, moved to environment variables using dotenv
- **index.js** had no error handling for database connection failures, added connection error logging
- **package.json** was missing a `start` script and had an unnecessary `i` dependency
- **package.json** was missing `bcrypt` and `dotenv` dependencies

## License

ISC
