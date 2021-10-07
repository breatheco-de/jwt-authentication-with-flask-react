# JWT Authentication With Flask & React.js

Almost every website in the world has user authentication, in this project you have to implement user authentication using the Python Flask framework for building a backend REST API and React.js and sessionStorage API for the front end web application.

The use of [this template/boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) is recomended to start the development, it already comes with the necesary setup and installation for start coding in one minute.

## 🗒️ Instructions

Implement an authentication system with the following parts:

1. **Signup**: The user must be able to pick its email, any password and submit the form, a new user must be created in the database and the user must be redirected to the login form afterwards.
2. **Login**: The user fills out its email and password and it's redirected to your dashboard after successfull authentication.
3. **Validation**: Any page considered "private" must always validate that the current user is valid, if not, the page must redirect the user back to login.
4. **Logout**: Any moment the user must be able to press "logout" in the navbar and it will get redirected back to the login path.

At least the following pages and react components must be implemented into the project:

| Path      | Component   | Functionality                                                     |
| --------- | ----------- | ----------------------------------------------------------------- |
| `/signup` | `<Signup>`  | Renders the signup form                                           |
| `/login`  | `<Login>`   | Renders the login form                                            |
| `/private`| `<Private>` | Validates that only authenticated users and render this component |

## 🌱 How to start coding this project:

Do not clone this repository.

1. The first step to start coding is cloning the [React.js + Flask API boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) on your local computer or opening it using gitpod.

a) If using Gitpod (recommended) you can clone the boilerplate by [clicking here](https://gitpod.io#https://github.com/4GeeksAcademy/react-flask-hello).

b) If working locally type the following command from your command line: `git clone https://github.com/4GeeksAcademy/react-flask-hello`.

💡 Remember to create a new repository, update the remote (`git remote set-url origin <your new url>`), and upload the code to your new repository using `add`, `commit` and `push`.

## More details about the authentication:

Usually an authentication system is implemented in 4 parts:

![Authentication Diagram](https://github.com/breatheco-de/jwt-authentication-with-flask-react/blob/main/.learn/login_diagram.jpeg?raw=true)

### User signup

At the beginning of every application that are no users or tokens, so the first step that makes sense to build is user signup.

1. The user navigates to the `/signup` path.

2. The React.js application (probably using the React Router library) will detect the route `/signup` and match with its corresponding React.js page component that will take care of rendering the signup HTML.

3. The user picks and writes an email and password and clicks submit.

4. The React.js page is listening to the onSubmit event, it gets triggered and the handleSubmit function fetches the email and password to the backend Pthon Flask API, probably doing a `POST /token` request with the email and password on the body payload.

### User login (start session)

This part of the process occurs only when new tokens have to be generated.

1. The user lands in the `myapplication.com/login` path.

2. The React.js application (probably using the React Router library) will detect the `/login` path and match it with its corresponding React.js page component, this page will take care of rendering the login form.

3. The user fills the login form and submits it.

4. The page is listening (waiting) for the form sumbit event to trigger, and it finally triggers because the user submite the form.

5. The page now retrieves the username and password information and fetch (`POST`) that data to the API.

6. The API validates that the username and password are correct and returns a `token` object.

7. The front-end application saves that token in the `sessionStorage`.

8. The front end application redirects to the `/private`.

### User logout (end session):

This process occurs when the user desires to logout.

1. Normally there is a button to log out somewhere in your application.

2. The user press that button and the onClick event handler is called.

3. The front-end application removes the token from the sessionStorage.

4. The front-end application redirects to the home page (public).

### Token Validation 

Any user can just type `/private` to attempt visiting a private page, that is why we need to implement a validation that prevents the anonymus users to see the content of this page, and we must redirect the user to `/login` or any other **public** page. This is usually how the process goes:

1. The user types any private URL, for example: myapplication.com/private

2. The React.js application (probably using the React Router library) will detect the route `/private` and match with its corresponding React.js page component that will take care of rendering the HTML.

3. Before rendering the HTML -and only because this is a private route- the component must verify that the sessionStorage contains the authenticated token, you normally would do that in the useEffect (component did mount) because you want to do it very early during the application loading.

4. If sessionStorage 👎 **does not** have the token, the current user is not considered to be logged in and the component must redirect to the login view.

5. If the sessionStorage 👍 does contain the token, the current user is successfully logged in and the rest of the `/private` view component is loaded.





