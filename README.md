# Taller Fork — Sistemas Operativos
**Pontificia Universidad Javeriana**  
Facultad de Ingeniería · Departamento de Ingeniería de Sistemas

**Integrantes:**
- David Antonio Pedraza Navarro
- Oscar Samuel Pinilla Alvira
- Johan Manuel Barreto Ramírez


**Docente:** John Corredor Franco

---

## Descripción

Programa en C que demuestra la creación de procesos y comunicación entre ellos en un entorno UNIX/Linux. El programa recibe dos archivos de texto con arreglos de enteros y distribuye los cálculos de sumatoria entre una jerarquía de 4 procesos usando `fork()` y `pipe()`.

**Jerarquía de procesos:**

```
Padre
 ├── Segundo hijo  →  calcula sumaB  →  envía al Padre
 └── Primer hijo
       └── Grand hijo  →  calcula sumaA  →  envía al Primer hijo
             (Primer hijo suma total y envía al Padre)
```

---

## Archivos del proyecto

| Archivo | Descripción |
|---|---|
| `main.c` | Punto de entrada, validación de argumentos y gestión de memoria |
| `ficheros.c / .h` | Lectura de archivos y cálculo de sumatorias |
| `procesos.c / .h` | Creación de procesos y comunicación por pipes |
| `Makefile` | Automatización de compilación |
| `archivo00.txt` | Arreglo de prueba A |
| `archivo01.txt` | Arreglo de prueba B |

---

## Compilación y ejecución

**Compilar:**
```bash
make
```

**Ejecutar:**
```bash
./tallerFork N1 archivo00.txt N2 archivo01.txt
```

> `N1` y `N2` indican cuántos elementos leer de cada archivo.

**Ejemplo con los archivos de prueba:**
```bash
./tallerFork 5 archivo00.txt 5 archivo01.txt
```

**Salida esperada:**
```
Arreglo A: 5 elementos desde 'archivo00.txt'
Arreglo B: 5 elementos desde 'archivo01.txt'

[Grand hijo   | PID ...] sumaA = 150
[Segundo hijo | PID ...] sumaB = 125
[Primer hijo  | PID ...] suma total = 275

[Padre         | PID ...] RESULTADOS
  sumaB  (fichero01)        = 125
  Suma total (fich00+fich01)= 275
```

> El orden de los mensajes de los procesos hijos puede variar entre ejecuciones — es comportamiento normal de la concurrencia.

**Limpiar compilación:**
```bash
make clean
```
