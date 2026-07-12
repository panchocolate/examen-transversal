def leer_opcion():
    while True:
        try:
            opcion = int(input("Ingrese opción: "))
            if 1 <= opcion <= 6:
                return opcion
            else:
                print("Debe seleccionar una opción válida")
        except ValueError:
            print("Debe seleccionar una opción válida")

def cupos_tipo(tipo, planes, inscripciones):
    total = 0
    for cod, datos in planes.items():
        if datos[1].lower() == tipo.lower():
            total += inscripciones[cod][1]
    print(f"El total de cupos disponibles es: {total}")

def busqueda_precio(p_min, p_max, planes, inscripciones):
    resultados = []
    for cod, datos_ins in inscripciones.items():
        precio = datos_ins[0]
        cupos = datos_ins[1]
        if p_min <= precio <= p_max and cupos > 0:
            nombre = planes[cod][0]
            resultados.append(f"{nombre}--{cod}")
    if resultados:
        resultados.sort()
        print(f"Los planes encontrados son: {resultados}")
    else:
        print("No hay planes en ese rango de precios.")

def buscar_codigo(codigo, diccionario):
    return codigo.upper() in diccionario

def actualizar_precio(codigo, nuevo_precio, inscripciones):
    if buscar_codigo(codigo, inscripciones):
        inscripciones[codigo.upper()][0] = nuevo_precio
        return True
    return False

def val_codigo(codigo, planes):
    return bool(codigo and codigo.strip() and not buscar_codigo(codigo, planes))

def val_nombre(nombre):
    return bool(nombre and nombre.strip())

def val_tipo(tipo):
    return tipo.lower() in ['mensual', 'trimestral', 'anual']

def val_duracion(duracion):
    return duracion > 0

def val_piscina(opcion):
    return opcion.lower() in ['s', 'n']

def val_clases(opcion):
    return opcion.lower() in ['s', 'n']

def val_horario(horario):
    return bool(horario and horario.strip())

def val_precio(precio):
    return precio > 0

def val_cupos(cupos):
    return cupos >= 0

def agregar_plan(codigo, nombre, tipo, duracion, acceso_piscina, incluye_clases, horario, precio, cupos, planes, inscripciones):
    cod_upper = codigo.upper()
    if buscar_codigo(cod_upper, planes):
        return False
    
    piscina_bool = True if acceso_piscina.lower() == 's' else False
    clases_bool = True if incluye_clases.lower() == 's' else False
    
    planes[cod_upper] = [nombre, tipo.lower(), duracion, piscina_bool, clases_bool, horario]
    inscripciones[cod_upper] = [precio, cupos]
    return True

def eliminar_plan(codigo, planes, inscripciones):
    cod_upper = codigo.upper()
    if buscar_codigo(cod_upper, planes):
        del planes[cod_upper]
        del inscripciones[cod_upper]
        return True
    return False

def main():
    planes = {
        'F001': ['Plan Básico', 'mensual', 1, False, False, 'libre'],
        'F002': ['Plan Full', 'mensual', 1, True, True, 'libre'],
        'F003': ['Plan Estudiante', 'trimestral', 3, False, True, 'tarde'],
        'F004': ['Plan Senior', 'trimestral', 3, True, False, 'mañana'],
        'F005': ['Plan Anual Pro', 'anual', 12, True, True, 'libre'],
        'F006': ['Plan Nocturno', 'mensual', 1, False, True, 'noche']
    }
    inscripciones = {
        'F001': [14990, 30],
        'F002': [22990, 10],
        'F003': [39990, 0],
        'F004': [35990, 6],
        'F005': [159990, 2],
        'F006': [18990, 15]
    }

    while True:
        print("\n========== MENÚ PRINCIPAL ==========")
        print("1. Cupos por tipo de plan")
        print("2. Búsqueda de planes por rango de precio")
        print("3. Actualizar precio de plan")
        print("4. Agregar plan")
        print("5. Eliminar plan")
        print("6. Salir")
        print("=====================================")
        
        opcion = leer_opcion()
        
        if opcion == 1:
            tipo = input("Ingrese tipo de plan a consultar: ")
            cupos_tipo(tipo, planes, inscripciones)
        elif opcion == 2:
            while True:
                try:
                    p_min = int(input("Ingrese precio mínimo: "))
                    p_max = int(input("Ingrese precio máximo: "))
                    if p_min >= 0 and p_max >= p_min:
                        busqueda_precio(p_min, p_max, planes, inscripciones)
                        break
                    else:
                        print("Debe ingresar valores válidos y el precio mínimo debe ser menor o igual al máximo")
                except ValueError:
                    print("Debe ingresar valores enteros")
        elif opcion == 3:
            continuar = 's'
            while continuar.lower() == 's':
                codigo = input("Ingrese código del plan: ")
                try:
                    nuevo_precio = int(input("Ingrese nuevo precio: "))
                    if val_precio(nuevo_precio):
                        if actualizar_precio(codigo, nuevo_precio, inscripciones):
                            print("Precio actualizado")
                        else:
                            print("El código no existe")
                    else:
                        print("El precio debe ser un número entero mayor que cero")
                except ValueError:
                    print("Debe ingresar valores enteros")
                continuar = input("¿Desea actualizar otro precio (s/n)?: ")
        elif opcion == 4:
            codigo = input("Ingrese código del plan: ")
            if not val_codigo(codigo, planes):
                print("Error: El código no puede estar vacío y no debe existir previamente.")
                continue
            nombre = input("Ingrese nombre del plan: ")
            if not val_nombre(nombre):
                print("Error: El nombre no puede estar vacío.")
                continue
            tipo = input("Ingrese tipo (mensual/trimestral/anual): ")
            if not val_tipo(tipo):
                print("Error: El tipo debe ser 'mensual', 'trimestral' o 'anual'.")
                continue
            try:
                duracion = int(input("Ingrese duración (meses): "))
                if not val_duracion(duracion):
                    print("Error: La duración debe ser mayor a cero.")
                    continue
            except ValueError:
                print("Error: Debe ingresar un valor entero para la duración.")
                continue
            piscina = input("¿Incluye acceso a piscina? (s/n): ")
            if not val_piscina(piscina):
                print("Error: Debe ingresar 's' o 'n'.")
                continue
            clases = input("¿Incluye clases grupales? (s/n): ")
            if not val_clases(clases):
                print("Error: Debe ingresar 's' o 'n'.")
                continue
            horario = input("Ingrese horario: ")
            if not val_horario(horario):
                print("Error: El horario no puede estar vacío.")
                continue
            try:
                precio = int(input("Ingrese precio: "))
                if not val_precio(precio):
                    print("Error: El precio debe ser mayor a cero.")
                    continue
            except ValueError:
                print("Error: Debe ingresar un valor entero para el precio.")
                continue
            try:
                cupos = int(input("Ingrese cupos: "))
                if not val_cupos(cupos):
                    print("Error: Los cupos deben ser mayores o iguales a cero.")
                    continue
            except ValueError:
                print("Error: Debe ingresar un valor entero para los cupos.")
                continue
            
            if agregar_plan(codigo, nombre, tipo, duracion, piscina, clases, horario, precio, cupos, planes, inscripciones):
                print("Plan agregado")
            else:
                print("El código ya existe")
        elif opcion == 5:
            codigo = input("Ingrese código del plan: ")
            if eliminar_plan(codigo, planes, inscripciones):
                print("Plan eliminado")
            else:
                print("El código no existe")
        elif opcion == 6:
            print("Programa finalizado.")
            break

if __name__ == "__main__":
    main()
