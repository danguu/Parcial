# Parcial

##Punto 1

-Solución iterativa  
```do
#include <stdio.h>

int main() {
    int num, i, factorial = 1;
    
    printf("Ingrese un numero entero: ");
    scanf("%d", &num);

    if (num < 0) {
        printf("El factorial no esta definido para numeros negativos.\n");
    } else {
        for (i = 1; i <= num; ++i) {
            factorial *= i;
        }
        printf("El factorial de %d es %d\n", num, factorial);
    }

    return 0;
}
```
-Solución recursiva 
```do
#include <stdio.h>

int factorial(int n) {
  if (n == 0) {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

int main() {
  int num;
  printf("Ingrese un numero entero: ");
  scanf("%d", &num);
  printf("El factorial de %d es %d\n", num, factorial(num));
  return 0;
}
```
- Comparación y respuesta
  
En términos de eficiencia, el programa iterativo es generalmente más rápido y eficiente que el programa recursivo, ya que no tiene el overhead de las llamadas recursivas y la creación de pilas de llamadas. Para mejorar la eficiencia del programa, se pueden considerar otros paradigmas de programación, como la programación dinámica o la programación funcional.

Programación dinámica:

Una forma de mejorar la eficiencia del programa en este caso, se podría crear un arreglo para almacenar los factoriales previamente calculados y reutilizarlos en lugar de recalcularlos.

Programación funcional:

Otra forma de mejorar la eficiencia en este caso, se podría utilizar una función que devuelva una lista de factoriales previamente calculados y luego se pueda utilizar esta lista para calcular el factorial de un número específico.

##Punto 2

-Solución imperativo 
```do
def bubble_sort(students):
    n = len(students)
    for i in range(n - 1):
        for j in range(n - i - 1):
            if students[j][1] < students[j + 1][1]:
                students[j], students[j + 1] = students[j + 1], students[j]
            elif students[j][1] == students[j + 1][1] and students[j][0] > students[j + 1][0]:
                students[j], students[j + 1] = students[j + 1], students[j]
    return students

# Ejemplo ouo
estudiantes = [
    ("Juan", 85),
    ("Daniel", 92),
    ("samuel", 92),
    ("Mari", 78),
    ("Luis", 85)
]

estudiantes_ordenados = bubble_sort(estudiantes)
print(estudiantes_ordenados)
```
-solución declarativo 
```do
import Data.List

data Student = Student { name :: String, grade :: Int } deriving (Show, Eq, Ord)

students :: [Student]
students = [  
  Student "Alm" 85,
  Student "Me" 92,
  Student "Estoy" 78,
  Student "Quedando" 92,
  Student "Dormido" 88
  ]

sortedStudents :: [Student]
sortedStudents = sortBy (\(Student _ g1) (Student _ g2) -> compare g2 g1) $ sortBy (\(Student n1 _) (Student n2 _) -> compare n1 n2) students

main :: IO ()
main = print sortedStudents
```
-Comparación 

El código en Haskell es más eficiente y legible que el código en Python. Sin embargo, el código en Python es más flexible y da más control sobre el proceso de ordenación. El código en Python utiliza un enfoque imperativo, es decir, se enfoca en describir cómo se debe realizar la ordenación. En cambio, el código en Haskell utiliza un enfoque declarativo, es decir, se enfoca en describir qué se quiere lograr.

##Punto 3

-Codigo 
```do
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definición de la estructura para almacenar la información del estudiante
typedef struct {
    char *nombre;
    char *apellido;
    unsigned int edad;
    char *ID;
    int *calificaciones;
    size_t num_calificaciones;
} Estudiante;

// Función para crear un nuevo estudiante
Estudiante *crear_estudiante(const char *nombre, const char *apellido, unsigned int edad, const char *ID, int *calificaciones, size_t num_calificaciones) {
    Estudiante *nuevo_estudiante = (Estudiante *)malloc(sizeof(Estudiante));

    if (nuevo_estudiante == NULL) {
        printf("Error al asignar memoria para el estudiante.\n");
        return NULL;
    }

    nuevo_estudiante->nombre = (char *)malloc(strlen(nombre) + 1);
    nuevo_estudiante->apellido = (char *)malloc(strlen(apellido) + 1);
    nuevo_estudiante->ID = (char *)malloc(strlen(ID) + 1);

    if (nuevo_estudiante->nombre == NULL || nuevo_estudiante->apellido == NULL || nuevo_estudiante->ID == NULL) {
        printf("Error al asignar memoria para los campos de texto.\n");
        free(nuevo_estudiante);
        return NULL;
    }

    strcpy(nuevo_estudiante->nombre, nombre);
    strcpy(nuevo_estudiante->apellido, apellido);
    strcpy(nuevo_estudiante->ID, ID);

    nuevo_estudiante->edad = edad;

    nuevo_estudiante->calificaciones = (int *)malloc(num_calificaciones * sizeof(int));
    if (nuevo_estudiante->calificaciones == NULL) {
        printf("Error al asignar memoria para las calificaciones.\n");
        free(nuevo_estudiante->nombre);
        free(nuevo_estudiante->apellido);
        free(nuevo_estudiante->ID);
        free(nuevo_estudiante);
        return NULL;
    }

    for (size_t i = 0; i < num_calificaciones; i++) {
        nuevo_estudiante->calificaciones[i] = calificaciones[i];
    }

    nuevo_estudiante->num_calificaciones = num_calificaciones;

    return nuevo_estudiante;
}

// Función para liberar la memoria de un estudiante
void liberar_estudiante(Estudiante *estudiante) {
    if (estudiante != NULL) {
        free(estudiante->nombre);
        free(estudiante->apellido);
        free(estudiante->ID);
        free(estudiante->calificaciones);
        free(estudiante);
    }
}

// Función para imprimir la información de un estudiante
void imprimir_estudiante(const Estudiante *estudiante) {
    if (estudiante != NULL) {
        printf("Nombre: %s %s\n", estudiante->nombre, estudiante->apellido);
        printf("Edad: %u\n", estudiante->edad);
        printf("ID: %s\n", estudiante->ID);
        printf("Calificaciones: ");
        for (size_t i = 0; i < estudiante->num_calificaciones; i++) {
            printf("%d ", estudiante->calificaciones[i]);
        }
        printf("\n");
    }
}

int main() {
    int calificaciones[] = {88, 80, 77};
    size_t num_calificaciones = sizeof(calificaciones) / sizeof(calificaciones[0]);

    Estudiante *estudiante = crear_estudiante("Daniel", "Ayala", 19, "1025321046", calificaciones, num_calificaciones);

    if (estudiante != NULL) {
        imprimir_estudiante(estudiante);

        // Calcular y mostrar el uso de memoria
        size_t memoria_usada = sizeof(Estudiante) + 
                               strlen(estudiante->nombre) + 1 + 
                               strlen(estudiante->apellido) + 1 + 
                               strlen(estudiante->ID) + 1 + 
                               num_calificaciones * sizeof(int);

        printf("Memoria utilizada: %zu bytes\n", memoria_usada);

        // Liberar memoria
        liberar_estudiante(estudiante);
    }

    return 0;
}
```
-Comparación 

La implementación en C utilizando el paradigma imperativo ofrece una mayor eficiencia en la asignación de memoria y un control preciso sobre la liberación de memoria, pero puede ser más compleja y propensa a errores. La implementación del paradigma declarativo ofrece una mayor abstracción y simplicidad, garantías de seguridad y reutilización de código, pero puede afectar la eficiencia en la asignación de memoria y el rendimiento en la creación de estructuras de datos.
