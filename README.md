<!--hide-->
# JWT Authentication With Flask & React.js
<!--endhide-->

Almost every website in the world has user authentication. In this project, you have to implement user authentication using the Python Flask framework for building a backend REST API and React.js, and *sessionStorage* API for the frontend web application.

## 📝 Instructions

Implement an authentication system with the following parts:

1. **Signup**: The user must be able to pick their email, a password and submit the form; a new user must be created in the database, then the user must be redirected to the login form afterwards.
2. **Login**: The user fills out their email and password, then it's redirected to the private dashboard after a successful authentication.
3. **Validation**: Any page considered "private" must always validate that the current user is valid; if not, the page must redirect the user back to the login page.
4. **Logout**: At any moment the user must be able to press "logout" in the navbar, and it will get redirected back to the login path.

At least the following pages and React components must be implemented into the project:

| Path       | Component   | Functionality                                                      |
| ---------  | ----------- | -----------------------------------------------------------------  |
| `/signup`  | `<Signup>`  | Renders the signup form                                            |
| `/login`   | `<Login>`   | Renders the login form                                             |
| `/private` | `<Private>` | Validates that only authenticated users can enter and renders this component |

<onlyfor saas="false" withBanner="false">
 
## 🌱 How to start this project

Do not clone this repository because we are going to be using a different template.

We recommend opening the `React.js + Flask API boilerplate` using a provisioning tool like [Codespaces](https://4geeks.com/lesson/what-is-github-codespaces) (recommended) or [Gitpod](https://4geeks.com/lesson/how-to-use-gitpod). Alternatively, you can clone it on your local computer using the `git clone` command.

This is the repository you need to open or clone:

```text
https://github.com/4GeeksAcademy/react-flask-hello
```

**👉 Please follow these steps on** [how to start a coding project](https://4geeks.com/lesson/how-to-start-a-project).


> 💡 Important: Remember to save and upload your code to GitHub by creating a new repository, updating the remote (`git remote set-url origin <your new url>`), and uploading the code to your new repository using the `add`, `commit` and `push` commands from the git terminal.

</onlyfor>

## More details about the authentication:

Usually, an authentication system is implemented in 4 parts:

![Authentication Diagram](https://github.com/breatheco-de/jwt-authentication-with-flask-react/blob/main/.learn/login_diagram.jpeg?raw=true)

### User signup

At the beginning of every application, there are no users or tokens, so the first step that makes sense to build is user signup.

1. The user navigates to the `/signup` path.
2. The React.js application (probably using the React Router library) will detect the route `/signup` and match it with its corresponding React.js page component, which will take care of rendering the signup HTML.
3. The user picks and writes an email and password and clicks submit.
4. The React.js page is listening for the `onSubmit` event; it gets triggered and the `handleSubmit` function fetches the email and password to the backend Python Flask API, probably doing a `POST /token` request with the email and password on the body's payload.

### User login (start session)

This part of the process occurs only when new tokens have to be generated.

1. The user lands in the `myapplication.com/login` path.
2. The React.js application (probably using the React Router library) will detect the `/login` path and match it with its corresponding React.js page component; this page will take care of rendering the login form.
3. The user fills out the login form and submits it.
4. The page is listening (waiting) for the form submit event to trigger, and it finally triggers because the user submits the form.
5. The page now retrieves the username and password information and fetch (POST) that data to the API.
6. The API validates that the username and password are correct and returns a `token` object.
7. The front-end application saves that token in the `sessionStorage`.
8. The front-end application redirects to the `/private`.

### User logout (end session)

This process occurs when the user desires to logout.

1. Normally, there is a button to log out somewhere in your application.
2. The user presses that button, and the `onClick` event handler is called.
3. The front-end application removes the token from the `sessionStorage`.
4. The front-end application redirects to the home page (public).

### Token Validation 

Any user can just type `/private` to attempt visiting a private page. That is why we need to implement a validation that prevents anonymous users from seeing the content of this page, and we must redirect the user to `/login` or any other **public** page. This is usually how the process goes:

1. The user types any private URL, for example: `myapplication.com/private`.
2. The React.js application (probably using the React Router library) will detect the route `/private` and match it with its corresponding React.js page component that will take care of rendering the HTML.
3. Before rendering the HTML -and only because this is a private route- the component must verify that the `sessionStorage` contains the authenticated token. You normally would do that in the `useEffect` because you want to do it very early during the application loading.
4. If `sessionStorage` 👎 **does not** have the token, the current user is not considered to be logged in and the component must redirect to the login view.
5. If the `sessionStorage` 👍 does contain the token, the current user is successfully logged in, and the rest of the `/private` view component is loaded.

This and many other projects are built by students as part of the 4Geeks Academy [Coding Bootcamp](https://4geeksacademy.com/us/coding-bootcamp) by [Alejandro Sanchez](https://twitter.com/alesanchezr) and many other contributors. Find out more about our [Full Stack Developer Course](https://4geeksacademy.com/us/coding-bootcamps/part-time-full-stack-developer), and [Data Science Bootcamp](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning).
 



