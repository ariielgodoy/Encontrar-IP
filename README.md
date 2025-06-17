# 🕵️‍♂️ Cómo Descubrir la IP de un Generador de Voltaje DC en tu Red Local
Recordar que lo que se necesita en el programa es el **HOSTNAME** del generador que sale en la pagina web del programa.
¿Necesitas conectar con tu generador de voltaje pero no tienes idea de cuál es su dirección IP? ¡No te preocupes! Esta guía te enseñará un método infalible para encontrarlo usando unos simples comandos en tu terminal.

---

## 📝 El Plan de Ataque

La estrategia es simple: vamos a "gritar" en la red para que todos los dispositivos nos respondan. Al hacerlo, nuestro ordenador actualizará su lista de "vecinos" conocidos (la tabla ARP), y ahí es donde encontraremos a nuestro generador.

---

## 📡 **Paso 1: Lanza una Llamada a Toda la Red (Ping Broadcast)**

El primer paso es enviar una señal a todos los dispositivos de tu red para que se presenten.

### 1. Conoce tu propia IP

Abre una terminal o **CMD** en Windows y ejecuta el siguiente comando para saber cuál es tu dirección IP actual:

```bash
ipconfig
```

Busca tu `Dirección IPv4`. Será algo parecido a `192.168.1.10`.

### 2. Construye la Dirección de Broadcast

Toma tu dirección IP y reemplaza el último número (el último octeto) por `255`. Esta es la dirección especial a la que todos los dispositivos de la red prestan atención.

> **Ejemplo:** Si tu IP es `192.168.1.10`, tu dirección de broadcast será `192.168.1.255`.

### 3. Ejecuta el Ping Broadcast

Ahora, envía un `ping` a esa dirección de broadcast. Esto obligará a todos los dispositivos, incluido tu generador, a responder, actualizando así la tabla ARP de tu PC.

```bash
ping 192.168.1.255
```
> **Nota:** En sistemas operativos como macOS o Linux, puede que necesites usar el flag `-b` para permitir el broadcast: `ping -b 192.168.1.255`.

---

## 🗺️ **Paso 2: Consulta el Mapa de tu Red (Tabla ARP)**

Tu ordenador ya ha conocido a todos los dispositivos cercanos. Ahora, solo tenemos que consultar esa lista.

### Muestra la Tabla ARP

En la misma terminal, ejecuta el comando `arp` con el flag `-a` para mostrar la tabla completa.

```bash
arp -a
```

Verás una lista de todas las `Direcciones de Internet` (IP) con sus correspondientes `Direcciones físicas` (MAC) que tu ordenador ha descubierto.

```
Interfaz: 192.168.1.10 --- 0x12
  Dirección de Internet   Dirección física      Tipo
  192.168.1.1             a1-b2-c3-d4-e5-f6     dinámico
  192.168.1.5             00-1a-2b-3c-4d-5e     dinámico  <-- ¿Quizás es este?
  192.168.1.23            f9-e8-d7-c6-b5-a4     dinámico  <-- ¿O este?
  192.168.1.255           ff-ff-ff-ff-ff-ff     estático
```

---

## 🎯 **Paso 3: ¡Ahí Estás! Identifica tu Generador**

Ya tienes la lista de sospechosos. Ahora solo queda identificar cuál de ellos es tu generador.

### Método 1: Por la Dirección MAC (El más profesional)

Muchos fabricantes de hardware usan un patrón específico en los primeros dígitos de la dirección MAC (conocido como OUI - Organizationally Unique Identifier). Si conoces el fabricante de tu generador (Ej: Chroma, Keysight, TDK-Lambda), puedes buscar su OUI y encontrar la MAC que coincida en la lista.

### Método 2: Prueba y Error (El más directo)

Si no conoces el patrón de la MAC, el método más rápido es simplemente probar las direcciones IP que has encontrado:

1.  Abre tu navegador web.
2.  Copia y pega cada una de las direcciones IP de la lista `arp -a` en la barra de direcciones.
3.  ¡La dirección que te muestre la interfaz web de tu generador de voltaje es la correcta!

✨ **¡Listo!** Ya tienes la dirección IP y puedes empezar a trabajar con tu generador, pero recordar que en el campo del programa que pone nombre del generador va el **HOSTNAME** de la pagina web.
