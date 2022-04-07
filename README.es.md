# Autenticación JWT con Flask y React.jsy

Casi todos los sitios web en el mundo tienen autenticación de usuarios, en este proyecto debes realizar una aplicación web implementando la autenticación de usuarios usando Python y el framework Flask para construir un back-end de REST API y React.js, y sessionStorage API para el Front-end.

El uso de [esta plantilla/boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) es recomendada para comenzar el desarrollo, ya viene preparada con todas las condiciones e instalaciones para comenzar a programar en un minuto.

## 🗒️ Instrucciones

Implementa un sistema de autenticación en las siguientes partes:

1. **Registro**: El usuario deberá poder colocar un correo, cualquier contraseña y enviar el formulario, un nuevo usuario debe ser creado en la base de datos y el usuario debe ser redireccionado al inicio de sesión luego de esto.
2. **Inicio de Sesión**: El usuario debe llenar su correo y contraseña y debe ser redirigido a un menu privado luego de que la autenticación sea éxitosa.
3. **Validación**: Cualquier página considerada "privada" siempre debe estar validando que el usuario actual es válido, si no, la página debe redirigir al inicio de sesión.
4. **Cierre de Sesión**: Cualquier momento que el usuario presione el "cierre de sesión" en la barra de navegación (navbar) se debe redirigir a la ruta del inicio de sesión.

Al menos las siguientes páginas y componentes de react deben ser implementados en el proyecto:

| Ruta      | Componente  | Funcionalidad                                                                |
| --------- | ----------- | -----------------------------------------------------------------            |
| `/signup` | `<Signup>`  | Renderizar formulario de registro                                            |
| `/login`  | `<Login>`   | Renderizar formulario de Inicio de sesión                                    |
| `/private`| `<Private>` | Validar que solo ingresen usuarios autenticados y renderizar este componente |

## 🌱 Como comenzar a programar este proyecto:

No clones este repositorio.

1. El primer paso para comenzar a programar es clonar el [React.js + Flask API boilerplate](https://github.com/4GeeksAcademy/react-flask-hello) en tu computadora o abriendo usando gitpod.

a) Si usas Gitpod (recomendado) tu puedes clonar la plantilla/boilerplate haciendo [click aquí](https://gitpod.io#https://github.com/4GeeksAcademy/react-flask-hello).

b) Si trabajas de forma local, tipea el siguiente comando en tu linea de comando o consola: `git clone https://github.com/4GeeksAcademy/react-flask-hello`.

💡 Recuerda crear un nuevo repositorio, actualiza el remoto (`git remote set-url origin <tu nueva url>`), y carga el código de tu nuevo repositorio usando `add`, `commit` y `push`.

## Mas detalles sobre la autenticación:

Usualmente un sistema de autenticación es implementado en 4 partes:

![Diagrama de Autenticación](https://github.com/breatheco-de/jwt-authentication-with-flask-react/blob/main/.learn/login_diagram.jpeg?raw=true)

### Registro de usuario

Al principio de cada aplicación no hay usuario o tokens, asi que el primer paso que hace sentido es crear un registro de usuario.

1. El usuario navega a la ruta `/signup`.
2. La aplicación de React.js (probablemente usando la libreria React Router) deberá detectar la ruta `/signup` y realizará emparejado con el correspondiente componente de pagina de React.js, esta página se encargará de representar el HTML del registro.
3. El usuario escoge y escribe un correo electrónico, una contraseña y hace clic en enviar.
4. La página de React.js esta a la espera de el evento onSubmit, este al activarse la función handleSubmit obtiene el email y contraseña de la API del Backend con python y flask, probablemente usanto una petición `POST /token` con el email y contraseña en el body payload.

### Inicio de sesión

Esta parte del proceso ocurre solo cuando los nuevos tokens fueron generados.

1. El usuario aterriza en la ruta miaplicacion.com/login.
2. La aplicación de React.js (probablemente usando la libreria React Router) deberá detectar la ruta `/login` y realizará un emparejado con el correspondiente componente de página de React.js, esta página se encargará de renderizar el formulario de inicio de sesión.
3. El usuario llena formulario de inicio de sesión y lo envía.
4. La página está esperando a que se active el evento de envío del formulario, y finalmente se activa porque el usuario envía el formulario.
5. La página ahora recopila la información del nombre de usuario y contraseña para subir (POST) la data a la API.
6. La API valida que nombre de usuario y contraseña sean correctos y regresa un objeto `token`.
7. El front-end de la aplicación guarda el token en el sessionStorage.
8. El front-end de la aplicación redirecciona a la ruta `/private`.

### Cierre de sesión

Este proceso ocurre cuando el usuario desea cerrar la sesión.

1. Normalmente hay un botón para el cierre de sesión en algún lado de la aplicación.
2. El usuario presiona el botón y el controlador de eventos onClick es llamado.
3. El front-end de la aplicación elimina el token del sessionStorage.
4. El front-end de la aplicación redirige a la página de inicio (público).

### Validación del Token

Cualquier usuario puede solo tipear `/private` para intentar visitar una página privada, por eso es que se necesita implementar una validación, para prevenir que usuarios anonimos vean el contenido de la página privada, y debemos redirigir al usuario a la ruta `/login` o a otra página **publica**. Asi es como usualmente es el proceso:

1. El usuario tipea cualquier URL privada, por ejemplo: myapplication.com/private
2. La aplicación de React.js (probablemente usando la libreria React Router) detectará la ruta `/private` y realizara un emparejado con el correspondiente componente de página de React.js que se encargará de renderizar el HTML.
3. Antes de renderizar el HTML -y solo porque esta es una ruta privada- el componente debe verificar que el sessionStorage contiene un token autenticado, normalmente esto se haria en el useEffect (component did mount) porque se quiere que se haga tan pronto la aplicación cargue.
4. Si el sessionStorage 👎 **no** tiene el token, el usuario actual no esta considerado como registrado y el componente debe redirigirlo a la vista del inicio de sesión.
5. Si el sessionStorage 👍 contiene el token, el actual usuario esta registrado exitosamente y el resto de la vista del componente `/private` es cargado.
