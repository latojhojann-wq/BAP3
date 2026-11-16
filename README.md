# Visor URL (Android)

App Android que pide una URL, la recuerda y la abre dentro de la app con permiso de cámara
(`getUserMedia`, `<input type="file" capture>`, escáneres de códigos con la cámara).

- Hecha con Capacitor 8. La pantalla inicial está en `www/index.html`.
- Permisos incluidos: cámara, micrófono, internet.
- Atrás (botón de Android) vuelve de la página abierta a la pantalla de la URL.
- Opción "Abrir automáticamente la última URL al iniciar" (desactivada por defecto).
- Botón "Probar cámara" para comprobar el permiso sin depender de ninguna página externa.

## Obtener el APK sin instalar nada (GitHub Actions)

1. Crea un repositorio nuevo en github.com (puede ser privado).
2. Sube TODO el contenido de esta carpeta, incluida la carpeta oculta `.github`
   (arrástrala con el explorador de archivos; si no aparece, activa "mostrar archivos ocultos").
3. En el repositorio entra a **Actions** > **Compilar APK** > **Run workflow**.
4. Al terminar (unos 5 a 8 minutos), abre la ejecución y descarga el artefacto **visor-url-apk**.
   Es un zip que contiene `app-debug.apk`.
5. Pasa el APK al teléfono, ábrelo y acepta "instalar apps de fuentes desconocidas" cuando lo pida.

## Compilar con Android Studio (alternativa)

1. Instala Node 22+ y Android Studio.
2. En esta carpeta: `npm install` y luego `npx cap sync android`.
3. `npx cap open android`, y en Android Studio: Build > Build APK(s).

## Cambios habituales

- **Nombre de la app**: `android/app/src/main/res/values/strings.xml` (`app_name`), y `appName` en `capacitor.config.json`.
- **Ícono**: reemplaza los archivos en `android/app/src/main/res/mipmap-*`.
- **URL fija**: en `www/index.html`, reemplaza el contenido del script por `window.location.href = 'https://tu-url';`.
- Tras cambiar `www/` ejecuta `npx cap sync android` (en GitHub Actions ya lo hace solo).

## Notas

- El APK generado es de depuración: sirve para instalar y usar directamente. Para publicar en
  Google Play hay que firmarlo con un keystore propio.
- La página abierta debe usar HTTPS para que el navegador interno entregue la cámara.
- Si la página que abres muestra su contenido dentro de un iframe de otro dominio, ese iframe
  también debe permitir la cámara. Si la página ya usa la cámara en Chrome del teléfono,
  debería funcionar igual aquí.
