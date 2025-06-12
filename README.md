# OAuth2 Login with GitHub in Spring Boot

This project demonstrates OAuth2 implementation in a Spring Boot application using GitHub as the authentication provider. It covers setting up OAuth2 client configurations, creating endpoints for login/logout, and displaying user details upon successful authentication.

## Project Overview

In this application, users can:
- Log in using their GitHub accounts.
- Access a customized home page displaying their GitHub profile and repository links.
- Log out securely, clearing session data.
- Revoke tokens in GitHub to test re-authorization flows.

### Key Concepts

- **OAuth2 Flow:** We leverage GitHub as the OAuth2 provider.
- **Session Management:** Ensure secure sessions with Spring Security.
- **User Interface (UI):** Simple UI built with Thymeleaf and Bootstrap.

## Prerequisites

- **Java 21**
- **Maven 3+**
- **Spring Boot 3.x**
- **GitHub Developer Account** (for creating OAuth App)

## Getting Started

### 1. Set Up GitHub OAuth Application

Create an OAuth application on GitHub:

1. Go to [GitHub Developer Settings](https://github.com/settings/developers).
2. Select **New OAuth App**.
3. Fill in details:
    - **Application name**: `ajika-app.com` (or any other name)
    - **Homepage URL**: `http://localhost:8080`
    - **Authorization callback URL**: `http://localhost:8080/login/oauth2/code/github`

4. Once created, save the **Client ID** and **Client Secret**.

### 2. Clone This Repository

Clone this project repository:

git clone `https://github.com/karangwaajika/oauth-github`


### 3. Set Up Configuration

Open `src/main/resources/application.yml` and add your GitHub OAuth2 credentials:

spring:
security:
oauth2:
client:
registration:
github:
client-id: <YOUR_CLIENT_ID>
client-secret: <YOUR_CLIENT_SECRET>
scope: read:user

### 4. Build and Run

Use Maven to build and run the application:

mvn clean install
mvn spring-boot:run

Visit `http://localhost:8080/login` to start the login process.

## Project Structure

### `pom.xml`

Includes the following dependencies:

- `spring-boot-starter-web`: Provides web application support.
- `spring-boot-starter-oauth2-client`: Manages OAuth2 login and authorization.
- `spring-boot-starter-thymeleaf`: Renders dynamic HTML templates.

### `application.yml`

Contains configuration for OAuth2 login:

- **Client ID** and **Client Secret** from GitHub OAuth.
- Scope set to `read:user` for accessing basic GitHub profile information.

### Security Configuration

Located in `SecurityConfig.java`:

- **Permit Access:** Sets `/login` and `/logout` as open paths.
- **OAuth2 Login Setup:** Defines a custom login page and redirects successful logins to `/home`.
- **Session Invalidation:** Clears session data upon logout.

### Controllers

#### `MyController.java`

- **/login**: Displays the login page.
- **/home**: Fetches user details and renders them on `home.html`.
- **/logout**: Ends the session and redirects to `logout.html`.
- **/error**: Displays error information if authentication fails.

### HTML Templates

1. **`login.html`** - Displays a button for GitHub login.
2. **`home.html`** - Displays user details (username, profile link, and repositories).
3. **`logout.html`** - Confirms user logout and provides a re-login option.
4. **`error.html`** - Displays error details for authentication issues.

---

## Usage Scenarios

### 1. User Login

- Access `http://localhost:8080/login`.
- Click on **Login via GitHub**.
- Upon successful authorization, users are redirected to the home page.

### 2. Re-login Without Re-Authorization

- After initial login, subsequent logins bypass re-authorization (session persists).

### 3. Token Revocation

- Revoke tokens from GitHub to test re-authorization.
- On re-login, users will need to authorize the app again.

---

## Future Enhancements

- Support for additional OAuth2 providers (Google, Facebook).
- Adding detailed error handling and user-friendly messages.
- Implementing authorization flows with custom roles and scopes.

## Contributing

If you'd like to contribute, please fork the repository and create a pull request. 
