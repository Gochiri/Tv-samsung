# DNS y privacidad en la UN50MU6100

Dos cosas que se hacen con el control remoto, sin instalar nada y sin riesgo:

1. Apagar el rastreo de lo que mirás y la publicidad personalizada.
2. Usar un DNS que bloquee servidores de publicidad y telemetría.

> Los nombres de los menús son los de Tizen 3.0 (2017) en español. Según la versión del firmware pueden
> variar un poco. Antes de cambiar algo, sacale una foto a cómo estaba.

## Parte 1: privacidad (5 minutos)

### Rastreo y publicidad

**Configuración → Soporte → Términos y política**:

| Opción | Dejar en |
|---|---|
| Servicios de información de visualización | Desactivado. Es el sistema que identifica lo que se ve en pantalla, incluso por HDMI o cable. |
| Publicidad basada en intereses | Desactivado |
| Servicio de reconocimiento de voz | Desactivado, si no usás comandos de voz |

Algunas opciones piden aceptar o rechazar términos. Rechazarlos no afecta la imagen ni las apps.

### Que no abra Smart Hub al prender

**Configuración → General → Funciones inteligentes**:

| Opción | Dejar en |
|---|---|
| Ejecución automática de Smart Hub | Desactivado. Al prender va a la última fuente, sin banners. |
| Ejecución automática de la última app | A gusto. Si lo activás, abre la última app que usaste. |

## Parte 2: DNS que bloquea publicidad (5 minutos)

El DNS es el "directorio" que la tele usa para encontrar servidores en internet. Si usás uno que filtra,
cuando la tele intenta contactar un servidor de publicidad o de telemetría, la consulta no se resuelve
y ese contenido no carga.

**Qué consigue:** menos banners en Smart Hub y menos telemetría de Samsung y de terceros.
**Qué no consigue:** **no** saca la publicidad de YouTube, porque YouTube la sirve desde sus propios
servidores. Para eso está [TizenTube](tizenbrew.md).

### Opción A: solo en la tele (la más simple)

1. **Configuración → General → Red → Estado de la red → Configuración de IP**.
2. **Configuración DNS** → **Ingresar manualmente**.
3. **Servidor DNS:** `94.140.14.14` ([AdGuard DNS](https://adguard-dns.io/), servicio público y gratuito).
4. **Aceptar** y esperá a que diga que está conectada a internet.

La configuración de IP y el resto de los campos quedan como estaban. Solo cambia el DNS.

### Opción B: en el router (protege a toda la casa)

En la configuración del router (normalmente `192.168.0.1` o `192.168.1.1` desde el navegador), buscá
**DHCP** o **DNS** y poné:

- DNS primario: `94.140.14.14`
- DNS secundario: `94.140.15.15`

Así se filtra en todos los dispositivos conectados: la tele, los celulares y las PCs. Cada router tiene
un menú distinto; si el tuyo es del proveedor de internet, a veces este ajuste viene bloqueado.

### Opción C: más control

- **[NextDNS](https://nextdns.io/)**: gratis hasta cierta cantidad de consultas por mes. Muestra qué
  bloqueó y permite agregar listas, por ejemplo una específica para Samsung. Te da una IP propia para
  poner en la tele o el router.
- **[Pi-hole](https://pi-hole.net/)** o **AdGuard Home**: un servidor de DNS en tu casa, por ejemplo en
  una Raspberry Pi. Es lo más completo, pero hay que mantenerlo.

## Si algo deja de funcionar

Algunos filtros bloquean de más: una app no carga, la tienda de Samsung no abre o falla el inicio de
sesión.

1. Volvé a **Configuración de IP → Configuración DNS → Obtener automáticamente**.
2. Si así funciona, el bloqueo era la causa. Con AdGuard DNS público no se pueden hacer excepciones;
   con NextDNS o Pi-hole sí podés permitir ese dominio puntual.

## Cómo deshacerlo

- **DNS:** Configuración de IP → Configuración DNS → **Obtener automáticamente**.
- **Privacidad:** volvé a activar las opciones de la Parte 1. La foto que sacaste al principio te dice
  cómo estaban.
