# Hito-1-trimestre

# Función para agregar un cliente al archivo "clientes.txt"
def agregar_cliente():
    # Solicitar información del cliente
    nombre = input("Nombre del cliente: ")
    direccion = input("Dirección del cliente: ")
    telefono = input("Número de teléfono del cliente: ")
    correo = input("Correo electrónico del cliente: ")

    # Crear una cadena con la información del cliente
    cliente = f"{nombre},{direccion},{telefono},{correo}\n"

    try:
        # Abrir el archivo en modo de escritura y agregar la información del cliente
        with open("clientes.txt", "a") as file:
            file.write(cliente)
        print("Cliente registrado exitosamente.")
    except Exception as e:
        # Capturar y manejar cualquier excepción que ocurra durante la escritura
        print(f"Error al agregar el cliente: {e}")

# Función para visualizar todos los clientes en el archivo "clientes.txt"
def visualizar_clientes():
    try:
        # Abrir el archivo en modo de lectura y leer todas las líneas
        with open("clientes.txt", "r") as file:
            clientes = file.readlines()
            # Mostrar cada cliente en una nueva línea
            for cliente in clientes:
                print(cliente)
    except FileNotFoundError:
        # Capturar y manejar la excepción si el archivo no se encuentra
        print("El archivo 'clientes.txt' no existe.")

# Función para buscar un cliente por nombre o dirección en el archivo "clientes.txt"
def buscar_cliente():
    # Solicitar la cadena a buscar
    buscar = input("Ingresa el nombre o dirección a buscar: ")

    try:
        # Abrir el archivo en modo de lectura y buscar la cadena en cada línea
        with open("clientes.txt", "r") as file:
            clientes = file.readlines()
            # Mostrar las líneas que contienen la cadena buscada
            for cliente in clientes:
                if buscar in cliente:
                    print(cliente)
    except FileNotFoundError:
        # Capturar y manejar la excepción si el archivo no se encuentra
        print("El archivo 'clientes.txt' no existe.")

# Función para eliminar un cliente del archivo "clientes.txt"
def eliminar_cliente():
    # Solicitar el nombre del cliente a eliminar
    eliminar = input("Ingresa el nombre del cliente a eliminar: ")

    try:
        # Abrir el archivo en modo de lectura y leer todas las líneas
        with open("clientes.txt", "r") as file:
            clientes = file.readlines()

        # Abrir el archivo en modo de escritura y escribir todas las líneas excepto la del cliente a eliminar
        with open("clientes.txt", "w") as file:
            for cliente in clientes:
                # Verificar si la línea contiene el nombre del cliente a eliminar
                if eliminar not in cliente:
                    file.write(cliente)
        print(f"Cliente '{eliminar}' eliminado exitosamente.")
    except FileNotFoundError:
        # Capturar y manejar la excepción si el archivo no se encuentra
        print("El archivo 'clientes.txt' no existe.")

# Función para realizar una compra y agregarla al archivo "compras.txt"
def realizar_compra():
    # Solicitar información de la compra
    nombre_cliente = input("Nombre del cliente que realiza la compra: ")

    # Validar que el nombre del cliente no esté vacío
    if not nombre_cliente:
        print("Error: El nombre del cliente no puede estar vacío.")
        return

    productos = input("Lista de productos comprados (separados por coma): ")

    # Validar que la lista de productos no esté vacía
    if not productos:
        print("Error: La lista de productos no puede estar vacía.")
        return

    # Solicitar información adicional para el costo de envío
    es_espanol = input("¿Es usted español? (Sí/No): ").lower()

    # Establecer el costo de envío basado en la respuesta
    if es_espanol == 'no':
        costo_envio = 20
    else:
        costo_envio = 0

    # Crear una cadena con la información de la compra
    compra = f"{nombre_cliente},{productos},Costo de envío: ${costo_envio}\n"

    try:
        # Abrir el archivo en modo de escritura y agregar la información de la compra
        with open("compras.txt", "a") as file:
            file.write(compra)
        print("Compra registrada exitosamente.")

        # Llama a la función de seguimiento de compra con los argumentos adecuados
        seguimiento_compra(nombre_cliente)
    except Exception as e:
        # Capturar y manejar cualquier excepción que ocurra durante la escritura
        print(f"Error al registrar la compra: {e}")

# Función para realizar el seguimiento de una compra
def seguimiento_compra(nombre_cliente):
    # Verificar si el nombre está en la lista de clientes
    with open('clientes.txt', 'r') as archivo_clientes:
        lista_clientes = [line.strip() for line in archivo_clientes]

    if nombre_cliente in lista_clientes:
        # Si el nombre está en la lista, notificar al cliente por correo electrónico
        print(f"Su pedido ha sido notificado en su correo electrónico, {nombre_cliente}.")
    else:
        # Si el nombre no está en la lista, no notificar
        print(f"El nombre {nombre_cliente} no está en la lista de clientes. No se enviará ninguna notificación.")

# Ejemplo de uso
nombre_cliente_input = input("Ingrese su nombre para realizar el seguimiento de la compra: ")
seguimiento_compra(nombre_cliente_input)

# Menú principal
while True:
    print("\nGestión de Clientes")  # Imprime el título del menú
    print("1. Agregar cliente")  # Opción para agregar un cliente
    print("2. Visualizar todos los clientes")  # Opción para ver todos los clientes
    print("3. Buscar cliente por nombre o dirección")  # Opción para buscar clientes
    print("4. Eliminar cliente")  # Opción para eliminar un cliente
    print("5.Realizar compra")
    print("6.Realizar un seguimiento de la compra")
    print("7. Salir")  # Opción para salir del programa
    opcion = input("Selecciona una opción: ")  # Solicita al usuario que seleccione una opción

    if opcion == "1":
        agregar_cliente()  # Llama a la función para agregar un cliente
    elif opcion == "2":
        visualizar_clientes()  # Llama a la función para visualizar todos los clientes
    elif opcion == "3":
        buscar_cliente()  # Llama a la función para buscar clientes
    elif opcion == "4":
        eliminar_cliente()  # Llama a la función para eliminar un cliente
    elif opcion == "5":
        realizar_compra()
    elif opcion == "6":
        seguimiento_compra()
    elif opcion == "7":
        break  # Sale del bucle y finaliza el programa
    else:
        print("Opción no válida. Inténtalo de nuevo.")  # Mensaje si la opción ingresada no es válida

   


