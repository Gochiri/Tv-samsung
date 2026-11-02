# TizenBrew + TizenTube en la UN50MU6100

[TizenBrew](https://github.com/reisxd/TizenBrew) es una app open source que se instala una sola vez en
la tele y después permite agregar "módulos" sin volver a pasar por la PC. El módulo más usado es
[TizenTube](https://github.com/reisxd/TizenTube): YouTube sin publicidad, con SponsorBlock (salta los
segmentos patrocinados), control de velocidad y DeArrow (títulos sin clickbait).

Funciona desde Tizen 3.0 (2017), así que la UN50MU6100 entra.

> Pasos tomados de la documentación oficial de TizenBrew y TizenTube (revisada en noviembre de 2026).
> Si algo no coincide, manda la [guía oficial](https://github.com/reisxd/TizenBrew/blob/main/docs/README.md).

## Qué necesitás

- La tele y una PC (Windows, macOS o Linux) conectadas **a la misma red**, sea por Wi-Fi o cable.
- La IP de la PC:
  - **Windows:** abrí `cmd`, escribí `ipconfig` y buscá "Dirección IPv4" (algo como `192.168.0.15`).
  - **macOS:** Ajustes del Sistema → Red → tu conexión → Detalles → Dirección IP.
  - **Linux:** `ip -4 addr` o `hostname -I`.
- Unos 20 minutos.

No hace falta cuenta de Samsung ni certificado: eso solo lo piden las teles con Tizen 7 o posterior.

## Paso 1: activar el Modo desarrollador en la tele

1. Con el control, abrí **Apps** (desde la barra de Smart Hub).
2. Estando en la pantalla de Apps, marcá **1 2 3 4 5** en el control. Si el control no tiene
   números, usá el teclado numérico que aparece en pantalla.
3. Aparece la ventana **Modo desarrollador**:
   - Poné **Modo desarrollador** en **Encendido**.
   - En **IP de la PC host**, escribí la IP de tu PC.
4. Tocá **Aceptar**.
5. Reiniciá la tele **manteniendo apretado el botón de encendido** del control hasta que veas el logo
   de Samsung. Apagarla y prenderla de forma normal no alcanza, porque solo entra en reposo.

Al volver a Apps vas a ver el texto "Modo desarrollador" arriba. Es normal.

## Paso 2: instalar TizenBrew desde la PC

1. Descargá el ejecutable para tu sistema desde
   [TizenBrewInstaller → Releases](https://github.com/reisxd/TizenBrewInstaller/releases/latest).
   Bajalo solo de ese enlace: hay copias con nombres parecidos.
2. Ejecutalo.
   - En **macOS o Linux** puede que tengas que darle permiso y correrlo desde la terminal:
     ```bash
     chmod +x tizenbrew-installer-*
     ./tizenbrew-installer-*
     ```
   - En **Windows**, si SmartScreen lo frena, "Más información" → "Ejecutar de todas formas".
3. Hacé clic en **Connect to TV** y escribí la IP de la tele. La encontrás en la tele en
   Configuración → General → Red → Estado de la red → Configuración de IP.
4. Hacé clic en **Install TizenBrew** y esperá a que diga **Package installed**.

Si aparece *"Could not connect to the SDB Daemon"*, revisá la IP de la tele, que la IP de la PC host
sea la de esta PC y que hayas hecho el reinicio largo del paso 1.

## Paso 3: dejar la IP de la PC host en `127.0.0.1`

TizenBrew necesita conectarse a sí mismo dentro de la tele, así que hay que cambiar la IP que pusiste
en el paso 1:

1. Volvé a **Apps** → marcá **1 2 3 4 5**.
2. Dejá el Modo desarrollador **encendido** y cambiá **IP de la PC host** a `127.0.0.1`.
3. **Aceptar** y reiniciá otra vez manteniendo apretado el botón de encendido.

Si te salteás este paso, TizenBrew muestra: *"Could not connect to the SDB Daemon. Are you sure you
changed the Host PC IP to 127.0.0.1?"*

**El Modo desarrollador tiene que quedar encendido siempre.** Si lo apagás, TizenBrew deja de andar.

## Paso 4: agregar TizenTube

1. Abrí **TizenBrew** desde Apps.
2. Apretá el botón **verde** del control para abrir el administrador de módulos (Module Manager).
3. Elegí **Add NPM Module**.
4. Escribí exactamente:
   ```
   @foxreis/tizentube
   ```
5. Confirmá. TizenTube aparece en la lista de TizenBrew; abrilo desde ahí.

Opcional: en los ajustes de TizenBrew, **Autolaunch Settings** abre TizenTube directo cada vez que
entrás a TizenBrew.

Importante: TizenTube se usa **desde TizenBrew**, no desde la app de YouTube de Samsung. Si abrís la
app original vas a seguir viendo publicidad.

## Otros módulos

Desde el mismo administrador de módulos podés sumar otros. Por ejemplo, un cliente de
[Jellyfin](https://jellyfin.org/) para ver tus propios videos desde una PC o servidor de casa. La
lista oficial de módulos está en el [README de TizenBrew](https://github.com/reisxd/TizenBrew).

## Si algo falla

| Problema | Qué probar |
|---|---|
| El instalador no encuentra la tele | Confirmá que las dos estén en la misma red, que la IP de la PC host sea la de **esta** PC y que hayas reiniciado manteniendo apretado el botón de encendido. Desactivá un momento el firewall o la VPN de la PC. |
| "Could not connect to the SDB Daemon" | Paso 3: IP de la PC host en `127.0.0.1` y reinicio largo. |
| "You can't launch modules while the service hasn't connected" | Esperá unos segundos después de abrir TizenBrew y volvé a intentar. |
| Un módulo desapareció después de reiniciar | Volvé a agregarlo con el botón verde → Add NPM Module. |
| TizenTube muestra publicidad | Seguramente abriste la app de YouTube de Samsung. Entrá por TizenBrew. |
| Video entrecortado | Probá en TizenBrew → User-Agent Settings con la opción por defecto. Esta tele es de 2017 y en 4K puede quedarse corta: bajá a 1080p. |

## Alternativa: TizenTube sin TizenBrew

Si solo te interesa YouTube, TizenTube también existe como app independiente. Se instala con
[Apps2Samsung](https://github.com/Apps2Samsung/Apps2Samsung/releases) y el archivo
**`TizenTubeOld.wgt`**, que es la versión para Tizen 3 a 5.5. Los archivos `TizenTubeCobalt*.wgt`
**no** sirven para esta tele. Los pasos están en la
[guía de instalación de TizenTube](https://github.com/reisxd/TizenTube/blob/main/docs/README.md).

## Cómo deshacerlo

1. Apps → mantené apretado el ícono de TizenBrew (o TizenTube) → **Eliminar**.
2. Apps → **1 2 3 4 5** → Modo desarrollador en **Apagado** → reinicio largo.

La tele queda exactamente como estaba. Ni TizenBrew ni TizenTube tocan el firmware.
