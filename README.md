import csv
import os

def agregarMunicipio(municipios):
    os.system('cls')
    nombre = input("Ingrese el nombre del municipio: ")
    habitantesRurales = int(input("Ingrese el número de habitantes rurales: "))
    habitantesUrbanos = int(input("Ingrese el número de habitantes urbanos: "))
    
    totalHabitantes = habitantesRurales + habitantesUrbanos
    porcentajeRural = (habitantesRurales / totalHabitantes) * 100
    porcentajeUrbano = (habitantesUrbanos / totalHabitantes) * 100
    
    if porcentajeUrbano < 40:
        categoria = "Rural"
    elif porcentajeUrbano < 60:
        categoria = "Semiurbana"
    else:
        categoria = "Urbana"
    
    municipio = {
        "nombre": nombre,
        "habitantesRurales": habitantesRurales,
        "habitantesUrbanos": habitantesUrbanos,
        "porcentajeRural": porcentajeRural,
        "porcentajeUrbano": porcentajeUrbano,
        "categoria": categoria
    }
    
    municipios.append(municipio)
    print("Municipio agregado exitosamente.")
    os.system('pause')
    os.system('cls')

def mostrarMunicipios(municipios):
    os.system('cls')
    if not municipios:
        print("No hay municipios registrados.")
        return

    for municipio in municipios:
        print(f"Nombre: {municipio['nombre']}; Habitantes Rurales: {municipio['habitantesRurales']}; "
              f"Habitantes Urbanos: {municipio['habitantesUrbanos']}; Porcentaje Rural: {municipio['porcentajeRural']:.2f}%; "
              f"Porcentaje Urbano: {municipio['porcentajeUrbano']:.2f}%; Categoría: {municipio['categoria']}")
    os.system('pause')
    os.system('cls')

def exportarCsv(municipios):
    if not municipios:
        print("No hay municipios para exportar.")
        return
    
    with open('municipios.csv', mode='w', newline='') as file:
        writer = csv.DictWriter(file, fieldnames=["nombre", "habitantesRurales", "habitantesUrbanos", "porcentajeRural", "porcentajeUrbano", "categoria"])
        writer.writeheader()
        for municipio in municipios:
            writer.writerow(municipio)
    
    print("Datos exportados exitosamente a municipios.csv.")

def main():
    municipios = []
    
    while True:
        print("\nMenu:")
        print("1. Agregar municipio")
        print("2. Mostrar municipios")
        print("3. Exportar datos a CSV")
        print("4. Salir")
        
        opcion = input("Seleccione una opción: ")
        
        if opcion == "1":
            agregarMunicipio(municipios)
        elif opcion == "2":
            mostrarMunicipios(municipios)
        elif opcion == "3":
            exportarCsv(municipios)
        elif opcion == "4":
            print("Saliendo del programa.")
            break
        else:
            print("Opción no válida. Intente nuevamente.")

if __name__ == "__main__":
    main()
