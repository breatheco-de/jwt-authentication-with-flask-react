# JWT Authentication With Flask & React.js

Almost every website in the world has user authentication, in this project you have to implement user authentication using the Python Flask framework for building a backend REST API and React.js and sessionStorage API for the front end web application.

The use of [this template/boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) is recomended to start the development, it already comes with the necesary setup and installation for start coding in one minute.

Usually an authentication system is implemented in 4 parts:

### Token Validation 

Any private view will have to always validate the user session like this:

1. The user types any private URL, for example: myapplication.com/private
2. The React.js application (probably the React Router library) will detect the route `/private` and match with its corresponding React.js page component that will take care of rendering the HTML.
3. Before rendering the HTML -and only because this is a private route- the component must verify that the sessionStorage contains the authenticated token, you normally would do that in the useEffect (component did mount) because you want to do it very early during the application loading.
4. If sessionStorage 👎 **does not** have the token, the current user is not considered to be logged in and the component must redirect to the login view.
5. If the sessionStorage 👍 does contain the token, the current user is successfully logged in and the rest of the `/private` view component is loaded.

### User login (start session)

This part of the process occurs only when new tokens have to be generated.

1. The user lands in the myapplication.com/login path.
2. The React.js application (probably using the React Router library) will detect the `/login` path and match it with its corresponding React.js page component, this page will take care of rendering the login form.
3. The user fills the login form and submits it.
4. The page is listening (waiting) for the form sumbit event to trigger, and it finally triggers because the user submite the form.
5. The page now retrieves the username and password information and fetch (POST) that data to the API.
6. The API validates that the username and password are correct and returns a `token` object.
7. The front-end application saves that token in the sessionStorage.
8. The front end application redirects to the `/private`.

### User logout (end session)

This process occurs when the user desires to logout.

1. Normally there is a button to log out somewhere in your application.
2. The user press that button and the onClick event handler is called.
3. The front-end application removes the token from the sessionStorage.
4. The front-end application redirects to the home page (public).




