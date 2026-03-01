# T.A.P-Piedra-Papel-o-Tijera-Movil

# Estructura completa del programa 

# 1. Importaciones
```bash
import flet as ft
import random
```
¿Qué está pasando aquí?

flet → es la librería que permite crear la interfaz gráfica.

random → se usa para que la computadora elija una opción al azar.

Sin random, la máquina no podría simular una decisión real.

# 2. Función principal main
```bash
def main(page: ft.Page):
```
¿Por qué existe esta función?

En Flet, todo comienza dentro de main.

page representa la ventana de la aplicación.

Aquí se construye toda la interfaz.

También se define la lógica que interactúa con los botones.

Es como el “contenedor principal” del programa.

# 3. Configuración inicial de la página
```bash
page.title = "Piedra, Papel o Tijera"
page.vertical_alignment = ft.MainAxisAlignment.CENTER
page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
```
¿Qué hace esto?

Cambia el título de la ventana.

Centra los elementos vertical y horizontalmente.

Esto no afecta la lógica del juego, solo la presentación visual.

# 4. Definimos las opciones del juego
```bash
opciones = ["Piedra", "Papel", "Tijera"]
```
¿Por qué aquí?

Porque:

Estas opciones se usarán en toda la función.

Son necesarias para que la máquina elija una al azar.

Aquí estamos modelando las reglas del juego en una estructura de datos.

# 5. Creamos los textos que mostrarán resultados
```bash
txt_resultado = ft.Text(size=20)
txt_eleccion_maquina = ft.Text(size=18)
```
¿Qué representan?

txt_resultado → mostrará si ganaste, perdiste o empataste.

txt_eleccion_maquina → mostrará qué eligió la computadora.

Importante:
Se crean antes porque luego los modificaremos dentro de la función jugar.

# 6. Creamos la función jugar

Aquí empieza la lógica real.

def jugar(e):

Esta función se ejecuta cada vez que el usuario presiona un botón.

6.1 Obtener la elección del jugador
```bash
eleccion_usuario = e.control.data
```
¿Qué significa?

e es el evento del botón.

e.control es el botón que fue presionado.

.data es el valor que le asignamos al botón.

Así sabemos qué eligió el usuario.

6.2 Generar elección aleatoria de la máquina
```bash
eleccion_maquina = random.choice(opciones)
```
Aquí usamos la lista creada antes.

random.choice() selecciona un elemento aleatorio.

Simulamos que la máquina “decide”.

6.3 Mostrar la elección de la máquina
```bash
txt_eleccion_maquina.value = f"La máquina eligió: {eleccion_maquina}"
```
Actualizamos el texto dinámicamente.

6.4 Comparar las elecciones (LÓGICA CENTRAL)
Caso 1 — Empate
```bash
if eleccion_usuario == eleccion_maquina:
    txt_resultado.value = "¡Empate!"
Caso 2 — El jugador gana
elif (
    (eleccion_usuario == "Piedra" and eleccion_maquina == "Tijera") or
    (eleccion_usuario == "Papel" and eleccion_maquina == "Piedra") or
    (eleccion_usuario == "Tijera" and eleccion_maquina == "Papel")
):
    txt_resultado.value = "¡Ganaste!"
```

Aquí evaluamos todas las combinaciones ganadoras del jugador.

Usamos:

and → ambas condiciones deben cumplirse.

or → basta con que una combinación sea verdadera.

Caso 3 — La máquina gana
```bash
else:
    txt_resultado.value = "Perdiste"
```

Si no fue empate ni victoria del jugador, automáticamente la máquina gana.

6.5 Actualizar la interfaz
```bash
page.update()
```

Esto es muy importante.

En Flet, cuando cambias valores de controles (.value), debes actualizar la página para que los cambios se reflejen visualmente.

Sin esto, el texto no cambiaría en pantalla.

# 7. Crear los botones
```bash
btn_piedra = ft.ElevatedButton(" Piedra", data="Piedra", on_click=jugar)
btn_papel = ft.ElevatedButton(" Papel", data="Papel", on_click=jugar)
btn_tijera = ft.ElevatedButton(" Tijera", data="Tijera", on_click=jugar)
```
Cada botón:

Tiene texto visible

Tiene un data oculto (la opción real)

Llama a jugar cuando se presiona

Aquí conectamos interfaz + lógica.

# 8. Agregar todo a la página
```bash
page.add(
    ft.Text("Elige una opción:", size=22),
    btn_piedra,
    btn_papel,
    btn_tijera,
    txt_eleccion_maquina,
    txt_resultado
)
```
Aquí ensamblamos la interfaz.

Ordenamos:

Texto inicial

Botones

Resultado máquina

Resultado final

# 9. Ejecutar la aplicación
```bash
ft.app(target=main)
```
Esto inicia la aplicación.

Le dice a Flet:

Ejecuta la función main para construir la app.

# Flujo completo del programa

Se ejecuta ft.app

Se llama a main

Se construye la interfaz

El usuario presiona un botón

Se ejecuta jugar

Se comparan elecciones

Se actualizan textos

Se actualiza la página

# En resumen

Tu programa tiene:

Una parte de configuración

Una parte de interfaz

Una función que contiene la lógica del juego

Una estructura condicional que modela reglas reales

Un mecanismo de actualización visual

# Ejecución del proyecto en iOS con Flet
Descripción

La aplicación fue desarrollada utilizando el framework Flet para Python, lo que permitió crear una interfaz gráfica interactiva sin necesidad de desarrollar código nativo para dispositivos móviles.

Para ejecutar el proyecto en un dispositivo iOS (iPhone), se utilizó la aplicación oficial Flet disponible en App Store, la cual permite conectarse a un servidor Flet en ejecución desde una computadora.

Proceso de ejecución en iOS
# 1️ Instalación de la aplicación en el dispositivo móvil

Se descargó e instaló la aplicación oficial Flet en el iPhone desde la App Store.

Esta aplicación funciona como un cliente que puede conectarse a una aplicación Flet en ejecución dentro de una red local.

# 2️ Ejecución del proyecto en la computadora

En la computadora (macOS), se abrió la terminal dentro de la carpeta del proyecto y se ejecutó el siguiente comando:
```
flet run main.py
```
Al ejecutar este comando:

Flet levanta un servidor local.

Se genera una dirección IP (por ejemplo: http://192.168.1.15:8550).

Se habilita la conexión desde otros dispositivos en la misma red WiFi.

# 3️ Conexión del dispositivo iOS

Una vez iniciado el servidor:

Se abrió la aplicación Flet en el iPhone.

Se ingresó la dirección IP mostrada en la terminal (o se escaneó el código QR generado).

El dispositivo se conectó al servidor local.

Al establecer la conexión, la interfaz del juego se mostró en el dispositivo móvil.

# Funcionamiento técnico

El proceso funciona bajo un modelo cliente-servidor:

La computadora actúa como servidor y ejecuta el código Python.

El iPhone actúa como cliente.

Cuando el usuario interactúa con la aplicación (por ejemplo, al presionar un botón), el evento se envía al servidor.

El servidor procesa la lógica del programa.

El resultado se devuelve al dispositivo móvil en tiempo real.

Este método permite probar la aplicación en un entorno móvil sin necesidad de compilar o generar una aplicación nativa (IPA).

# Requisitos para la conexión

Ambos dispositivos deben estar conectados a la misma red WiFi.

El servidor debe estar activo mientras se utiliza la aplicación en el móvil.

No es necesario generar un archivo instalable para realizar pruebas.

# Codigo completo 
```
import flet as ft
import random

def main(page: ft.Page):

    page.title = "Juego: Piedra, Papel o Tijera"
    page.padding = 40
    page.theme_mode = ft.ThemeMode.LIGHT

    opciones = ["Piedra", "Papel", "Tijera"]

    # Texto resultado
    txt_maquina = ft.Text("La máquina aún no elige", size=18)
    txt_resultado = ft.Text("Aquí el resultado", size=22, weight=ft.FontWeight.BOLD)

    # Función del juego
    def jugar(e):
        eleccion_usuario = e.control.data
        eleccion_maquina = random.choice(opciones)

        txt_maquina.value = f"La máquina eligió: {eleccion_maquina}"

        if eleccion_usuario == eleccion_maquina:
            txt_resultado.value = "¡Empate!"
        elif (
            (eleccion_usuario == "Piedra" and eleccion_maquina == "Tijera") or
            (eleccion_usuario == "Papel" and eleccion_maquina == "Piedra") or
            (eleccion_usuario == "Tijera" and eleccion_maquina == "Papel")
        ):
            txt_resultado.value = "¡Ganaste! "
        else:
            txt_resultado.value = "Perdiste "

        page.update()

    # Botones
    btn_piedra = ft.ElevatedButton("Piedra", data="Piedra", on_click=jugar)
    btn_papel = ft.ElevatedButton("Papel", data="Papel", on_click=jugar)
    btn_tijera = ft.ElevatedButton("Tijera", data="Tijera", on_click=jugar)

    page.add(
        ft.Column(
            [
                ft.Text("Piedra, Papel o Tijera", size=26, weight=ft.FontWeight.BOLD),
                ft.Text("Elige una opción:"),
                ft.Row([btn_piedra, btn_papel, btn_tijera], spacing=20),
                ft.Divider(),
                txt_maquina,
                txt_resultado,
            ],
            spacing=20
        )
    )

ft.app(target=main)
```
# Programa en Macos
<img width="806" height="604" alt="Captura de pantalla 2026-03-01 a la(s) 17 42 00" src="https://github.com/user-attachments/assets/aa9a994f-97fa-42d8-8d1c-02ff6df71988" />

# QR para correr en ios
<img width="1143" height="994" alt="Captura de pantalla 2026-03-01 a la(s) 17 38 24" src="https://github.com/user-attachments/assets/11126976-496e-4a44-b98f-0ab8ca7803b3" />

# Programa en ios 
<img width="1284" height="2778" alt="image" src="https://github.com/user-attachments/assets/d9b349ea-1e88-440f-b77b-1f8b4301e342" />

