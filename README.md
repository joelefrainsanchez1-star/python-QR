import random
import pyqrcode
import png


detalleCompras = [[],[],[],[],[],[]]

def menuOpciones():
    print("---------- MENU ---------")
    print("Que accion desea realizar? ")
    print("* 1) Registrar Pedidos")
    print("* 2) Mostrar Pedidos")
    print("* 3) Mostrar detalle del Pedido")
    print("* 4) Eliminar pedido")
    print("* 5) Salir del sistema")
    return int(input("Ingresar una opcion: "))

def ingresarProducto():
    print("Ingresar datos del cliente: ")
    nombre = input("NOMBRE: ")
    apellido = input("APELLIDO: ")
    telefono = input("TELEFONO: ")
    direccion = input("DIRECCION: ")
    detalleCompras[0].append(nombre)
    detalleCompras[1].append(apellido)
    detalleCompras[2].append(telefono)
    detalleCompras[3].append(direccion)
    detalleCompras[4].append(random.randint(1000, 9999))
    print("\t\t\tSeleccione el paquete oftimatico a contratar\n" \
        "1) Opcion 1: PC + Monitor = $500\n" \
        "2) Opcion 2: PC + Monitor 4K = $2000\n" \
        "3) Opcion 3: Lapotp UltraProIA = $1500\n" \
        "4) Worstation servidor = $3000\n")
    opcionPedido = int(input("Ingrese una opcion: "))
    if (opcionPedido == 1): costo = 500*1.15
    elif (opcionPedido == 2): costo = 2000*1.15
    elif (opcionPedido == 3): costo = 1500*1.15
    elif (opcionPedido == 4): costo = 3000*1.15
    detalleCompras[5].append(costo)
    print("pedido registrado exitosamente")

def mostrarPedido(i):
    print("Datos del cliente: ")
    print("Nombre: ", detalleCompras[0][i])
    print("Apellido: ", detalleCompras[1][i])
    print("Telefono: ", detalleCompras[2][i])
    print("Direccion: ", detalleCompras[3][i])
    print("Codigo de pedido: ", detalleCompras[4][i])
    print("total a pagar: ", detalleCompras[5][i])

def mostrarPedido1():
    if len(detalleCompras[0]) == 0:
        print("No hay pedidos registrados")
        return
    else:
        for columna in range(len(detalleCompras[0])):
            mostrarPedido(columna)
            pagoQRpedido(columna)


def pagoQRpedido(i):
    textoPago = f"Datos del pago * codigo del pedido {detalleCompras[4][i]}\nPago fina: ${detalleCompras[5][i]}\n"
    nombreArchivo= "Codigo QR.png"
    codigoQR = pyqrcode.create(textoPago)
    codigoQR.png(nombreArchivo, scale = 8)

def mostrarDetalleDelPedido():
    if len(detalleCompras[0]) == 0:
        print("No hay pedidos registrados")
        return
    else:
        codigo = int(input("Ingresar el codigo del pedido: "))
        if codigo in detalleCompras[4]:
            codigoIndex = detalleCompras[4].index(codigo)
            mostrarPedido(codigo)
        else:
            print("El odigo no existe")

def eliminarPEdido():
    codigo = int(input("Ingresar el codigo del pedido: "))
    if codigo in detalleCompras[4]:
        codigoIndex = detalleCompras[4].index(codigo)
        for i in range(len(detalleCompras[4])):
            detalleCompras[i].pop(codigoIndex)
    else:
        print("El odigo no existe")
        return



def main():
    opcion = 0
    while (opcion != 5):
        opcion = menuOpciones()
        match opcion:
            case 1:
                ingresarProducto()
                continue
            case 2:
                mostrarPedido1()
                continue
            case 3:
                mostrarDetalleDelPedido()
                continue
            case 4:
                eliminarPEdido()
                continue
            case 5:
                print("Saliendo del sistema")
            case default:
                print("opcion incorrecta")
                continue

main()
