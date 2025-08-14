<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Notificación con corazón</title>
  <style>
    body { font-family: system-ui, sans-serif; padding: 2rem; }
    button { padding: .7rem 1rem; margin-right: .5rem; border-radius: .6rem; border: 1px solid #ddd; cursor: pointer; }
  </style>
</head>
<body>
  <h1>Notificación con corazón ❤️</h1>
  <p>1) Da permiso, 2) prueba ahora o programa en 5s.</p>

  <button id="perm">Dar permiso</button>
  <button id="now">Mostrar ahora ❤️</button>
  <button id="in5">Mostrar en 5s ❤️</button>

  <script>
    const soportaNotificaciones = 'Notification' in window;

    async function pedirPermiso() {
      if (!soportaNotificaciones) {
        alert('Tu navegador no soporta notificaciones.');
        return;
      }
      const estado = await Notification.requestPermission();
      if (estado === 'granted') {
        mostrar('¡Permiso concedido! 💖');
      } else {
        alert('Necesitas conceder permiso para mostrar notificaciones.');
      }
    }

    function mostrar(body = 'Aquí va tu corazón ❤️') {
      if (!soportaNotificaciones) {
        alert('Tu navegador no soporta notificaciones.');
        return;
      }
      if (Notification.permission === 'granted') {
        new Notification('¡Ping de amor! ❤️', {
          body: body,
          // Puedes añadir un icono si tienes una URL: icon: 'icono.png'
        });
      } else {
        alert('Primero pulsa "Dar permiso".');
      }
    }

    document.getElementById('perm').addEventListener('click', pedirPermiso);
    document.getElementById('now').addEventListener('click', () => mostrar('¡Hola! Aquí está tu corazón ❤️'));
    document.getElementById('in5').addEventListener('click', () => {
      setTimeout(() => mostrar('Recordatorio con ❤️'), 5000);
      alert('Programada para 5 segundos.');
    });
  </script>
</body>
</html>
