# Modelos Econométricos SIS-3540 para HP Prime

Programa para la calculadora **HP Prime (G2)** que resuelve, paso a paso y con el mismo procedimiento de la bibliografía de la materia, los temas de **Modelos Econométricos (SIS-3540)**: regresión lineal simple y múltiple, correlación, heterocedasticidad, autocorrelación y multicolinealidad.

> **Estado del proyecto:** en desarrollo. Se trabaja **un módulo por vez**; cada entrega se prueba en el simulador antes de pasar a la siguiente (ver [Estado actual](#estado-actual)).

---

## Contenido

1. [Características](#características)
2. [Módulos y submódulos](#módulos-y-submódulos)
3. [Estructura del repositorio](#estructura-del-repositorio)
4. [Entorno de desarrollo](#entorno-de-desarrollo)
5. [Instalación con HP Connectivity Kit](#instalación-con-hp-connectivity-kit)
6. [Uso](#uso)
7. [Ejemplos de prueba](#ejemplos-de-prueba)
8. [Especificaciones de diseño](#especificaciones-de-diseño)
9. [Normas de desarrollo y compatibilidad HP PPL](#normas-de-desarrollo-y-compatibilidad-hp-ppl)
10. [Lecciones técnicas aprendidas](#lecciones-técnicas-aprendidas)
11. [Estado actual](#estado-actual)
12. [Bibliografía y créditos](#bibliografía-y-créditos)

---

## Características

- **Pantalla completa:** todo se dibuja sobre los gráficos (`G1`) y se muestra con `BLIT_P`. No se usan `INPUT` ni `MSGBOX`, que generan ventanas pequeñas.
- **Menú principal** con los módulos y un submenú por módulo, basado en los subtítulos del formulario.
- **Procedimiento idéntico a la bibliografía:** en las pruebas de hipótesis se muestran todos los pasos (hipótesis, α, estadístico de prueba, valor crítico de tablas, criterio de rechazo, valor calculado y decisión).
- **Valores de tablas de distribución** (t, F, χ², Z, corridas, Durbin-Watson) visibles en la solución, con su nombre, grados de libertad y α.
- **Tablas ANOVA** dibujadas como tabla, con celdas, bordes y todos sus valores.
- **Matrices** dibujadas como matrices (corchetes y filas/columnas alineadas), nunca como valores sueltos.
- **Gráficas** de dispersión, curva ajustada y residuos, con escalado automático a toda la pantalla.
- **Modelos no lineales** (exponencial y potencial) en los módulos 1, 2 y 3, a elección del usuario. El modelo estimado queda activo y todos los submódulos del módulo trabajan con él.
- **Ingreso de datos tipo hoja de cálculo:** tabla editable a pantalla completa, pensada para llenarse tan fácil como una tabla de Excel.
- **Nivel de significancia configurable:** el valor global de α se puede cambiar desde el menú principal o desde Datos y modelo; las pruebas e intervalos del módulo usan el valor guardado.
- **Táctil y teclado:** se maneja con flechas, `ENTER` y `ESC`, y también tocando la pantalla.
- **Colores resaltantes y consistentes** (ver [paleta](#paleta-de-colores)).

---

## Módulos y submódulos

| Módulo | Tema del formulario | Contenido |
|---|---|---|
| **1** | Tema 1: Regresión lineal simple | Datos y modelo, 1.1 IC para β0, 1.2 IC para β1, 1.3 Predicción (interpolación y extrapolación), 1.4 Utilidad del modelo (T), 1.5 Estadístico F y ANOVA, 1.6 Prueba de linealidad, 1.7 Modelos no lineales |
| **2** | Tema 2: Regresión lineal múltiple | Datos y modelo, 2.1 Método matricial, 2.2 IC para βi, 2.3 Prueba de hipótesis para βi, 2.4 Poder predictivo (ANOVA), 2.5 Predicción, 2.6 Adición de variables (F) |
| **3** | Tema 4: Correlación lineal | Datos y modelo, 3.1 a 3.13 (correlación simple, múltiple y parcial, inferencias, intervalos, matrices) y mejor modelo de primer orden |
| **4** | Tema 5: Heterocedasticidad, autocorrelación y multicolinealidad | Gráficas Ŷ-e² y eᵢ₋₁ vs eᵢ, Goldfeld-Quandt, corridas (n<15 y n>15), Durbin-Watson, prueba de correlación |

> La regresión polinomial (Tema 3 del formulario) no es un módulo aparte; queda pendiente de definir si se integra como submódulo del Módulo 2.

---

## Estructura del repositorio

```text
.
├── README.md
├── bibliografia/            # Bibliografía de cada tema (PDF)
│   ├── tema-1_regresion-lineal-simple.pdf
│   ├── tema-2_regresion-lineal-multiple.pdf
│   ├── tema-4_correlacion-lineal.pdf
│   └── tema-5_heterocedasticidad-autocorrelacion-multicolinealidad.pdf
├── formulario/              # Formulario de la materia con el que se trabaja
│   └── FORMULARIO_SIS_3540_COMPLETO.pdf
├── src/                     # Código fuente en texto (UTF-8), versionable
│   ├── MENUPRIN.hpprgm.txt
│   ├── MOD1.hpprgm.txt
│   └── ...
├── programas/               # Archivos .hpprgm listos para cargar (UTF-16 LE con BOM, CRLF)
│   ├── MENUPRIN.hpprgm
│   ├── MOD1.hpprgm
│   └── ...
├── utilidades/              # Programas de diagnóstico
│   ├── TECLAS.hpprgm        # Muestra los códigos de tecla
│   └── TOCAR.hpprgm         # Muestra lo que devuelve el táctil (MOUSE)
└── docs/
    └── PROMPT_DE_TRABAJO.md # Especificaciones usadas para desarrollar cada módulo
```

**Convención de nombres:** los archivos `.hpprgm.txt` de `src/` son la fuente editable; los `.hpprgm` de `programas/` se generan a partir de ellos convirtiéndolos a UTF-16 LE con BOM y finales de línea CRLF.

> **Nota sobre la bibliografía:** los PDF llevan marca de agua de su autor. Antes de publicar el repositorio, conviene verificar que se tiene permiso para compartirlos, o mantener el repositorio **privado**.

---

## Entorno de desarrollo

| Elemento | Detalle |
|---|---|
| Calculadora | HP Prime (G2) |
| Simulador | Calculadora virtual HP Prime, software **2.4.2** (build 2026-09-09, revisión 15751), CAS 1.5.0, MicroPython 1.9.4 |
| Sistema operativo | Windows 11 |
| Transferencia de archivos | HP Connectivity Kit |
| Lenguaje | HP PPL |
| Formato de entrega | `.hpprgm` en UTF-16 LE con BOM y finales de línea CRLF |
| Pantalla | 320 × 240 píxeles |

---

## Instalación con HP Connectivity Kit

1. Abre el **HP Connectivity Kit** y conecta la calculadora virtual (o la HP Prime física por USB).
2. En el panel izquierdo selecciona tu calculadora y entra a la sección de programas.
3. Arrastra los archivos `.hpprgm` de la carpeta `programas/` a la lista de programas.
4. **Orden de carga:** primero los módulos (`MOD1`, `MOD2`, ...) y al final `MENUPRIN`, porque el menú llama a las funciones exportadas por los módulos.
5. En la calculadora pulsa **Shift + 1** (catálogo de programas), elige `MENUPRIN` y ejecútalo, o escribe `MENUPRIN()` en la pantalla de inicio.
6. Si cambias un archivo, borra primero la versión anterior del programa en la calculadora o confirma que se sobrescriba.

### Verificar errores de sintaxis

En el catálogo de programas abre el programa en el editor y usa la opción **Verificar** (*Check*) del menú inferior. Marca la línea con el error y muestra su mensaje.

---

## Uso

1. Ejecuta `MENUPRIN()`.
2. Elige un módulo con las flechas y `ENTER`, o tocándolo en pantalla.
3. En el submenú abre el primer ítem, **Datos y modelo**, para cargar la muestra y elegir el modelo (lineal, exponencial o potencial).
4. Abre los demás submódulos; todos trabajan con los datos y el modelo activos.

**Controles**

| Acción | Teclado | Táctil |
|---|---|---|
| Moverse en listas | Flechas arriba/abajo | Tocar el ítem |
| Abrir | `ENTER` | Tocar el ítem |
| Volver | `ESC` | Botón **VOLVER** |
| Desplazar listas largas | Flechas | Botones **SUBIR** y **BAJAR** |

**Códigos de tecla** (obtenidos con `TECLAS`)

| Tecla | Código | Tecla | Código |
|---|---|---|---|
| Arriba | 2 | 4 / 5 / 6 | 37 / 38 / 39 |
| Abajo | 12 | 1 / 2 / 3 | 42 / 43 / 44 |
| Esc | 4 | 0 | 47 |
| Enter | 30 | 7 / 8 / 9 | 32 / 33 / 34 |

---

## Ejemplos de prueba

Valores esperados según la bibliografía (verificados con un cálculo independiente en Python):

| Ejercicio | Modelo | b1 | b0 |
|---|---|---|---|
| Ej. 1 (n=11) | Lineal | 1,809 | 6,414 |
| Ej. 4/5 (n=12) | Lineal | 0,963 | −1,112 |
| Ej. 4/5 (n=12) | Exponencial | 0,21811 | 0,9707 |
| Ej. 6 Oruro (n=15) | Potencial | −0,84298 | 528,58 |

Otros resultados de referencia del Tema 1:

- Ej. 2: IC 90 % para β1 = [0,704 ; 2,913]; predicción en X0 = 2,2 (extrapolación): [8,94 ; 11,83].
- Ej. 3: F calculado = 9,0 frente a F crítico = 5,12 (rechaza H0, el modelo tiene poder predictivo).
- Ej. 4: F de linealidad = 3,628 frente a 4,53 (acepta H0, la dependencia es lineal).
- Ej. 6: F de linealidad = 13,382 frente a 4,37 (rechaza H0, la dependencia no es lineal).

---

## Especificaciones de diseño

### Requisitos obligatorios

1. **Pantalla completa:** dibujar en `G1` (`DIMGROB_P(G1,320,240,color)` al inicio) con `RECT_P` y `TEXTOUT_P`, y mostrar con `BLIT_P(G0,G1)`. No usar `INPUT`, `MSGBOX` ni ventanas emergentes.
2. **Gráficas** de los datos y de las tablas (dispersión, curva ajustada, residuos), con escalado automático a toda la pantalla.
3. **Mismo procedimiento que la bibliografía**, en el mismo orden y notación. Las pruebas de hipótesis llevan todos los pasos:
   1. H0 y H1
   2. α
   3. Estadístico de prueba, valor crítico de tablas y criterio de rechazo
   4. Valor calculado
   5. Decisión
4. **Valores de tablas de distribución** (t, F, χ², Z, corridas, Durbin-Watson) en la solución, con nombre, grados de libertad y α.
5. **Tablas ANOVA** como tabla, con celdas, bordes y todos sus valores: fuente de variación, SC, gl, CM, F calculado y F crítico.
6. **Matrices** como matrices (corchetes y filas/columnas alineadas), nunca como valores sueltos ni separados por `/`.
7. **Colores resaltantes y consistentes** (ver paleta).
8. **Modelos no lineales** (exponencial y = b0·e^(b1·x) y potencial y = b0·x^b1, según el formulario 1.7) en los módulos 1, 2 y 3, además del lineal. El modelo estimado queda activo y todos los submódulos trabajan con él, linealizando con logaritmos y devolviendo los resultados en la escala original cuando corresponda.
9. **Interfaz** con flechas, `ENTER` y `ESC`, y también táctil (botones SUBIR, VOLVER y BAJAR en las listas largas).
10. **Ingreso manual de tablas** en cada módulo, con diseño de tabla y tan fácil de llenar como una tabla de Excel.
11. **Tamaño de letra** moderado y adecuado a la pantalla de 320 × 240 (se ajusta con las pruebas en el simulador).

### Paleta de colores

| Uso | Color |
|---|---|
| Títulos | Amarillo |
| Resultados | Verde |
| Valores de tablas | Cian |
| Decisiones | Verde (acepta/correcto) o rojo (rechaza/alerta) |

---

## Normas de desarrollo y compatibilidad HP PPL

### 1. Declaración explícita de variables globales

Toda variable global que se use, lea, modifique o comparta entre funciones o programas debe declararse explícitamente al inicio del archivo, antes de las funciones, con `EXPORT` e inicialización.

No se debe depender de la creación implícita de globales mediante asignaciones dentro de funciones, porque puede provocar errores de sintaxis o de reconocimiento de identificadores al compilar.

```pascal
EXPORT RmT:=0;
EXPORT RmX:={};
EXPORT RmY:={};

EXPORT RmCalcular()
BEGIN
  RmT:=1;
END;
```

### 2. Variables locales

Las variables que solo se necesitan dentro de una función se declaran como `LOCAL`. **Máximo 8 variables por declaración `LOCAL`**: si la función necesita más, se usan varias declaraciones.

```pascal
LOCAL ssr,sse,sst,n,k,t0,f0,s2;
LOCAL xm,ym,sxx,syy;
```

### 3. Organización y modularización

Funciones pequeñas, organizadas por responsabilidad. Se separan:

- Captura y validación de datos
- Cálculos matemáticos
- Procesamiento de resultados intermedios
- Generación de tablas
- Presentación de resultados
- Menús y navegación

Siempre que convenga, las funciones reciben los datos como parámetros para depender menos de globales compartidas.

### 4. Identificadores

Nombres descriptivos, consistentes y exclusivos de cada módulo. Se evitan nombres reservados, identificadores ambiguos y la reutilización accidental de variables entre programas. Renombrar una variable no basta como solución a un error de compilación sobre variables globales: primero se verifica que esté declarada explícitamente.

### 5. Dependencias y orden de compilación

Los módulos que exportan funciones se compilan **antes** que los programas que dependen de ellos. Se verifica que toda función llamada exista, esté exportada y tenga exactamente el mismo nombre en el programa que la llama.

### 6. Verificación incremental

Cada módulo se compila y prueba por separado antes de integrarlo al menú principal. Ante un error de sintaxis se aísla el problema con programas de prueba mínimos, cambiando una sola condición por prueba. No se hacen cambios masivos sin identificar antes la causa.

### 7. Compatibilidad con el entorno

Se considera el entorno de ejecución: HP Prime Virtual Calculator, versión del software, firmware, sintaxis PPL y restricciones del compilador. Una solución no se da por buena por su apariencia sintáctica; toda modificación distingue entre código **revisado**, **compilado** y **probado en ejecución**.

### 8. Criterio de entrega

Un módulo se considera terminado solo cuando:

1. Compila sin errores.
2. Sus funciones principales se ejecutaron.
3. Sus resultados se comprobaron contra la bibliografía.
4. No afecta negativamente a los módulos que dependen de él.
5. Se conserva una copia de la versión anterior antes de cambios importantes.

---

## Lecciones técnicas aprendidas

- `G1` debe crearse con `DIMGROB_P` antes de dibujar; si no, la pantalla sale en blanco.
- No usar `GETKEY` junto con `MOUSE`: `GETKEY` consume los toques. Las teclas se leen con `ISKEYDOWN` y el táctil con `MOUSE`.
- Las funciones auxiliares se definen antes de usarse; solo se marca `EXPORT` lo que se llama desde fuera del programa.
- Máximo 8 variables por declaración `LOCAL`.
- Declarar explícitamente las variables globales (ver normas).
- El tamaño de fuente debe ser moderado: una fuente grande desborda la pantalla de 320 × 240.

---

## Estado actual

| Componente | Estado |
|---|---|
| Menú principal (`MENUPRIN`) | Funcional en el simulador; falta verificar el táctil |
| Módulo 1: Datos y modelo (`MOD1`) | Implementado en el código; pendiente de compilación y prueba final en simulador |
| Módulo 1: submódulos 1.1 a 1.7 | Implementados: IC para β0 y β1, predicción, utilidad T, ANOVA F, prueba de linealidad y modelos exponencial/potencial. Configuración de α compartida. Pendiente de compilación y validación en simulador |

| Módulo 2 | Pendiente |
| Módulo 3 | Pendiente |
| Módulo 4 | Pendiente |
| Editor de datos tipo hoja de cálculo | Implementado en el código; pendiente de prueba en simulador |
| Gráficas | Pendiente |

**Siguiente paso:** compilar y probar `MOD1` y `MENUPRIN` en HP Prime Virtual Calculator 2.4.2, contrastar los resultados de 1.1 a 1.7 con los ejercicios de la bibliografía y corregir cualquier incompatibilidad detectada antes de iniciar el Módulo 2.

---

## Bibliografía y créditos

- **Formulario:** *Formulario SIS-3540*, Univ. Jhonatan Pally Cotaña.
- **Bibliografía de la materia:* Rubén Medinaceli O.
- **Materia:** Modelos Econométricos, SIS-3540.
- **Autor del programa:** *Univ. Barrionuevo Delgado ANgel*