<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chimbitas.rp - Registro y Login</title>
    <link rel="stylesheet" href="styles.css">
    <style>
        /* Estilos adicionales */
        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #0c0d0e;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            position: relative; /* Agrega posicionamiento relativo para el contenedor */
        }

        h1 {
            font-size: 24px;
            margin-bottom: 20px;
            color: #333;
        }

        .server-logo {
            position: absolute; /* Posiciona el logo */
            top: 10px; /* Ajusta la posición desde la parte superior */
            right: 10px; /* Ajusta la posición desde la parte derecha */
            width: 50px; /* Ajusta el ancho del logo según sea necesario */
            height: auto; /* Mantiene la proporción de la imagen */
        }
        
        /* Estilos de la imagen */
        .server-logo img {
            width: 100%;
            height: auto;
            border-radius: 50%;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="logo.png" alt="Logo del servidor" class="server-logo">
        <h1>Chimbitas Roleplay - Registro y Login</h1>
        <form id="loginForm">
            <h2>Iniciar Sesión</h2>
            <input type="text" id="loginUsername" placeholder="Usuario">
            <br>
            <input type="password" id="loginPassword" placeholder="Contraseña">
            <br>
            <button type="button" onclick="login()">Iniciar Sesión</button>
            <p>¿No tienes una cuenta? <a href="#" onclick="showRegister()">Regístrate</a></p>
        </form>
        <form id="registerForm" style="display: none;">
            <h2>Registrarse</h2>
            <input type="text" id="registerUsername" placeholder="Usuario">
            <br>
            <input type="email" id="registerEmail" placeholder="Correo Electrónico">
            <br>
            <input type="password" id="registerPassword" placeholder="Contraseña">
            <br>
            <button type="button" onclick="register()">Registrarse</button>
            <p>¿Ya tienes una cuenta? <a href="#" onclick="showLogin()">Iniciar Sesión</a></p>
        </form>
    </div>

    <script>
        // Verificar si hay datos de usuarios en el almacenamiento local
        var users = JSON.parse(localStorage.getItem('users')) || [];

        function showRegister() {
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('registerForm').style.display = 'block';
        }

        function showLogin() {
            document.getElementById('loginForm').style.display = 'block';
            document.getElementById('registerForm').style.display = 'none';
        }

        function login() {
            var username = document.getElementById('loginUsername').value;
            var password = document.getElementById('loginPassword').value;

            var userExists = users.find(function(user) {
                return user.username === username && user.password === password;
            });

            if (userExists) {
                document.getElementById('loginUsername').value = '';
                document.getElementById('loginPassword').value = '';
                alert('¡Bienvenido ' + username + '!');
                // Redirigir a la página 2 después del login
                window.location.href = 'index2.html';
            } else {
                alert('Esta cuenta no existe.');
            }
        }

        function register() {
            var username = document.getElementById('registerUsername').value;
            var email = document.getElementById('registerEmail').value;
            var password = document.getElementById('registerPassword').value;

            // Verificar si el usuario ya existe
            var userExists = users.find(function(user) {
                return user.username === username;
            });

            if (userExists) {
                alert('El nombre de usuario ya está en uso.');
                return;
            }

            // Agregar el nuevo usuario
            users.push({ username: username, email: email, password: password });

            // Guardar usuarios en el almacenamiento local
            localStorage.setItem('users', JSON.stringify(users));

            document.getElementById('registerUsername').value = '';
            document.getElementById('registerEmail').value = '';
            document.getElementById('registerPassword').value = '';

            alert('¡Registro exitoso! Por favor, inicia sesión.');
            showLogin();
        }
    </script>
</body>
</html>


