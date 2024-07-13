# OAuth Authentication with Express.js, Passport.js, and PostgreSQL

This project demonstrates how to set up a secure user authentication system using Express.js, Passport.js, and PostgreSQL. It includes local authentication with email and password as well as OAuth authentication with Google.

## Features

- User registration and login using email and password
- OAuth authentication with Google
- Secure password hashing with bcrypt
- Session management with express-session
- PostgreSQL for user data storage

## Prerequisites

- Node.js
- PostgreSQL
- Google Developer Account for OAuth credentials

## Setup

### Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

### Install Dependencies

```bash
npm install
```

### Configure Environment Variables

Create a `.env` file in the root of your project and add the following environment variables:

```env
GOOGLE_CLIENT_ID=""
GOOGLE_CLIENT_SECRET=""
SESSION_SECRET=""
PG_USER=""
PG_HOST=""
PG_DATABASE=""
PG_PASSWORD="+"
PG_PORT=""
```

### Set Up PostgreSQL

1. **Create Database and Table:**

```sql
CREATE DATABASE users;

\c users

CREATE TABLE usersData (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL
);
```

### Get Google OAuth Credentials

1. Go to the [Google Developers Console](https://console.developers.google.com/).
2. Create a new project or select an existing project.
3. Go to the "Credentials" tab and click "Create Credentials" > "OAuth 2.0 Client IDs".
4. Configure the OAuth consent screen and set up your OAuth 2.0 Client ID.
5. Add the following URIs to your Authorized Redirect URIs:
   - `http://localhost:3003/auth/google/secrets`

Copy the `Client ID` and `Client Secret` to your `.env` file.

### Run the Application

```bash
npm start
```

### Access the Application

Open your browser and go to `http://localhost:3003`.

## Routes

- `GET /`: Home page
- `GET /login`: Login page
- `GET /register`: Registration page
- `GET /logout`: Logout route
- `GET /secrets`: Protected page (only accessible to authenticated users)
- `GET /auth/google`: Initiates Google OAuth authentication
- `GET /auth/google/secrets`: Google OAuth callback

## Project Structure

- `index.js`: Main application file
- `views/`: Directory containing EJS templates
- `public/`: Directory for static files

## Authentication Flow

1. **Registration**:
   - User provides email and password.
   - Password is hashed using bcrypt and stored in PostgreSQL.
   - User is redirected to the protected page upon successful registration.

2. **Login**:
   - User provides email and password.
   - Password is verified using bcrypt.
   - User is redirected to the protected page upon successful login.

3. **Google OAuth**:
   - User is redirected to Google for authentication.
   - Upon successful authentication, user information is retrieved from Google.
   - If the user does not exist in the database, a new user record is created.
   - User is redirected to the protected page.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
