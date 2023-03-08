# Login with token

Cuando almacenamos el token en LocalStorage desde el front, lo hacemos para poder mantener iniciada la sesión. Sin embargo, tener token no implica tener los datos del usuario.

Para conseguir esto, tendremos que tener un método LoginwithToken desde el back. Este método se encargará de decodificar el token antiguo y devolver los datos de usuario y un nuevo token. De esta manera, también podemos incluir caducidad en los tokens.
