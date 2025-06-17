# ⚡ Cómo conocer la IP de un generador de voltaje DC en tu red local

## 🧭 Paso 1: Obtener tu dirección IP

Abre la terminal de **Windows (CMD)** y ejecuta:


Anota la **dirección IPv4** de tu adaptador de red. Por ejemplo:


---

## 📡 Paso 2: Hacer un *ping* al broadcast

Reemplaza el último octeto por `255`, y lanza un ping:


Esto envía un mensaje de broadcast en tu red. Aunque no siempre obtendrás respuestas visibles, tu PC aprenderá las direcciones MAC gracias a **ARP**, el protocolo de resolución de direcciones.

> 🔍 ARP actúa a nivel de **enlace** (switch) y actualiza internamente la tabla de direcciones.

---

## 🧠 ¿Qué estamos haciendo realmente?

Lo que buscamos es **forzar a tu PC a llenar su tabla ARP**, que es donde se guardan las asociaciones entre **IPs** y **MACs** de los dispositivos en la red local.

---

## 📋 Paso 3: Consultar la tabla ARP

Una vez que hayas enviado el ping de broadcast, ejecuta en la terminal:


Verás una lista como esta:


---

## 🔍 Paso 4: Identificar al generador

Si conoces el **prefijo de la dirección MAC** de tu generador, podrás identificarlo fácilmente. Si no lo conoces, prueba cada IP que aparece con un navegador o herramienta compatible.

Por ejemplo:


Esto puede abrir la interfaz de configuración del generador, o mostrar datos útiles sobre él.

> ✅ **Consejo:** Muchos generadores tienen un identificador MAC reconocible por el fabricante. Puedes buscar su OUI (Organizationally Unique Identifier) en [https://macvendors.com/](https://macvendors.com/).

---

## 🧩 Conclusión

Este proceso es útil cuando:

- No conoces la IP asignada al generador
- No puedes acceder a la configuración del router
- No hay DHCP bindings visibles

Y funciona en cualquier entorno LAN donde ARP esté activo.

📌 **Nota:** Este método no siempre funciona si el generador no responde a ARP o si está en una VLAN distinta.
