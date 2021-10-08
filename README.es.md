# Autenticación JWT con Flask y React.js

Casi todos los sitios web del mundo tienen autenticación de usuario, en este proyecto deberás implementar la autenticación de usuario utilizando el framework Python Flask para construir una API REST de backend y React.js y una API de sessionStorage para la aplicación web de front-end.

Te recomendamos que uses [este template/boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) para comenzar e desarrollo ya que tiene todas los setup e instalaciones necesarias para empezar a codificar en un minuto.

## 🗒️ Instrucciones

Implementa un sistema de autenticación con las siguientes partes:

1. **Signup**: El usuario debe poder elegir su correo electrónico, cualquier contraseña y enviar el formulario, se debe crear un nuevo usuario en la base de datos y luego se debe redirigir al usuario al formulario de inicio de sesión.

2. **Login**: El usuario ingresa su correo electrónico y su contraseña y es redireccionado al panel de control (dashboard) luego de una autenticación exitosa.

3. **Validation**: Cualquier página considerada como "privada" siempre debe validar al usuario, sino la página web debe redireccionar al usuario de regreso al **login**.

4. **Logout**: En cualquier momento el usuario debe poder hacer en clic en **logout** en la barra de navegación (navbar) y ser redireccionado a **login**.


Como mínimo, las siguientes vistas y componentes react deben implementarse en este proyecto:


|Path (tuta)| Componente   | Functionalidad                                                   |
| --------- | ----------- | ----------------------------------------------------------------- |
| `/signup` | `<Signup>`  | Muestra el formulario para registrarse                            |
| `/login`  | `<Login>`   | Muestra el formulario para ingresar                               |
| `/private`| `<Private>` | Valida a los usuarios autenticados y muestra este componente      |

## 🌱 Cómo empezar a codificar este proyecto:

No clones este repositorio.

1. El primer paso es clonar [el boilerplate React.js + Flask API ](https://github.com/4GeeksAcademy/react-flask-hello) en tu computador localmente o abrirlo con Gitpod:

a) Si usas Gitpod (recomendado), puedes clonar el texto estándar haciendo clic [aquí](https://gitpod.io#https://github.com/4GeeksAcademy/react-flask-hello).

b) Si trabajas localmente, escribe lo siguiente en tu línea de comando: `git clone https://github.com/4GeeksAcademy/react-flask-hello`.

+ 💡 Recuerda crear un nuevo repositorio, actualizar el remoto (`git remote set-url origin <su nueva url>`) y actualizar el código en tu nuevo repositorio usando `add`,`commit` y `push`.

## Más detalles sobre la autenticación:

Por lo general, un sistema de autenticación se implementa en 4 partes:

![Authentication Diagram](https://github.com/breatheco-de/jwt-authentication-with-flask-react/blob/main/.learn/login_diagram.jpeg?raw=true)

### Registro de usuario (signup):

Al comienzo de cada aplicación que no son usuarios o tokens, por lo que el primer paso que tiene sentido construir es el registro del usuario.

1. El usuario navega a la ruta (path) `/signup`.

2. La aplicación React.js (probablemente usando la librería React Router) detectará la ruta `/signup` y la hará coincidir con su componente de página React.js que se encargará de renderizar el HTML del registro.

3. El usuario escoge y escribe un correo electrónico y una contraseña y hace clic en enviar(submit).

4. La página React.js está escuchando el evento `onSubmit`, que gatilla/activa y la función `handleSubmit` busca (fetch) el correo electrónico y la contraseña en la API de backend Python Flask, probablemente haciendo una solicitud `POST/token` con el correo electrónico y la contraseña en el cuerpo de carga útil (body payload).

### Inicio de sesión de usuario (login)

Esta parte del proceso ocurre solo cuando se deben generar nuevos tokens.

1. El usuario llega a la ruta por ejemplo `myapplication.com/login`.

2. La aplicación React.js (probablemente usando la librería React Router) detectará la ruta `/login` y la emparejará con su componente de página React.js correspondiente, esta vista se encargará de renderizar el formulario de inicio de sesión.

3. El usuario llena el formulario de inicio de sesión y lo envía.

4. La página está escuchando (esperando) que se active/gatille el evento de `sumbit` del formulario y, finalmente se activa cuando el usuario envía el formulario.

5. La página ahora recupera la información de nombre de usuario y contraseña y envía (`POST`) esos datos de la API.

6. La API valida que el nombre de usuario y la contraseña sean correctos y devuelve un objeto `token`.

7. La aplicación front-end de guarda ese `token` en `sessionStorage`.

8. La aplicación front-end redirecciona a `/private`.

### Cierre de sesión del usuario (logout)

Este proceso ocurre cuando el usuario desea cerrar la sesión.

1. Normalmente debe haber un botón para cerrar sesión en algún lugar de tu aplicación.

2. El usuario presiona ese botón y se llama al event handler `onClick`.

3. La aplicación front-end elimina el `token` de `sessionStorage`.

4. La aplicación front-end redirecciona a la página de inicio (pública).

### Validación de tokens 

Cualquier usuario puede simplemente escribir `/private` para intentar visitar una página privada, es por eso que debemos implementar una validación que evite que los usuarios anónimos vean el contenido de esta página, y debemos redireccionar al usuario a `/login` o a cualquier otra página **pública**. Por lo general, así es como se desarrolla el proceso:

1. El usuario escribe cualquier URL privada, por ejemplo: `myapplication.com/private`

2. La aplicación React.js (probablemente usando la librería React Router) detectará la ruta `/private` y hará que coincida con su componente de página React.js que se encargará de renderizar el HTML.

3. Antes de renderizar el HTML, y solo porque se trata de una ruta privada, el componente debe verificar que `sessionStorage` contenga el `token` autenticado, normalmente `useEffect` (component did mount) lo hace pero tu querrás hacerlo muy temprano durante carga de la aplicación.

4. Si `sessionStorage` 👎 **no** tiene el `token`, no se considera que el usuario actual haya iniciado sesión y el componente debe redirigir a la página de inicio de sesión.

5. Si `sessionStorage` 👍 contiene el `token`, el usuario actual ha iniciado sesión correctamente y el resto del componente de vista `/private` está cargado.
