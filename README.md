# HP Prime – Modelos Econométricos (SIS-3540) - ESTADISTICA ll (MAT-1136)

Programa en **PPL (HP Prime Programming Language)** para resolver ejercicios de **regresión lineal simple, regresión lineal múltiple y correlación lineal**, siguiendo el procedimiento del formulario de la materia *Modelos Econométricos SIS-3540*: hipótesis, α, estadístico, criterio de rechazo, valor calculado y decisión.

> **Estado del proyecto:** 🟡 fase de planteamiento y diseño. Todavía no hay código; este README describe lo que se construirá.

---

## Objetivo

Que el estudiante capture **una sola vez** la tabla de datos de un ejercicio (Y, X1, X2, ..., Xk) y pueda entrar directamente al submódulo que el ejercicio pida (intervalo de confianza, predicción, prueba t, ANOVA, correlación parcial, etc.), con la salida presentada igual que en el formulario.

## Entorno

| Elemento | Detalle |
|---|---|
| Emulador de desarrollo | HP Prime Virtual Calculator 2.4.2 |
| Calculadora objetivo | HP Prime G2 |
| Lenguaje | PPL (Python de la Prime solo si hiciera falta) |
| Pantalla | 320 × 240 px |

## Estructura del menú

```
MENÚ PRINCIPAL
├── Tema 1: Regresión lineal simple
│   ├── Datos (ver / editar / cargar)
│   ├── 1.1 IC para β0
│   ├── 1.2 IC para β1
│   ├── 1.3 Predicción (interpolación / extrapolación)
│   ├── 1.4 Utilidad del modelo (prueba t)
│   ├── 1.5 Prueba F y tabla ANOVA
│   ├── 1.6 Prueba de linealidad
│   └── 1.7 Modelos no lineales (exponencial, potencial)
├── Tema 2: Regresión lineal múltiple
│   ├── Datos
│   ├── 2.1 Método matricial (A, g, b, A⁻¹)
│   ├── 2.2 IC para los βi
│   ├── 2.3 Pruebas de hipótesis sobre βi
│   ├── 2.4 Poder predictivo (F y ANOVA)
│   ├── 2.5 Predicción
│   └── 2.6 Adición de variables (F parcial)
├── Tema 4: Correlación lineal
│   └── 3.1 a 3.13 (simple, múltiple, parciales, "mejor modelo")
└── Configuración (α por defecto, decimales, modo examen/estudio)
```

> La numeración de las secciones **respeta la del formulario** (el Tema 4 usa 3.1–3.13), para que coincida con la hoja que se tiene al lado.

## Alcance

**Incluido**

- Tema 1: regresión lineal simple.
- Tema 2: regresión lineal múltiple.
- Tema 4: correlación lineal simple, múltiple y parcial.
- Asistente guiado **"Mejor modelo de primer orden"**.

**Fuera de alcance por ahora**

- Tema 3 (regresión polinomial): usa las mismas pruebas de los temas 1 y 2; se podrá agregar después.
- Tema 5 (heterocedasticidad, autocorrelación, multicolinealidad): en pausa hasta verlo en clase.
- Gráficos (dispersión, residuos): fase posterior.
- Ingreso directo de sumas (Σx, Σy, ...): los ejercicios vienen como tablas.
- Guardar varios ejercicios a la vez: se maneja una tabla de datos por tema.

## Asistente "Mejor modelo de primer orden"

Selección hacia adelante basada en correlación parcial:

1. Estimación del modelo con todas las X (2.1).
2. Matriz de correlación lineal simple (3.4).
3. La X con mayor correlación con Y entra si su prueba F es significativa (1.5).
4. Matriz de correlación parcial con esa X como variable de control (3.11).
5. Entra **solo** la de mayor correlación parcial si su prueba F es significativa (3.12).
6. Se repite con las variables ya incluidas como controles (3.11).
7. Se detiene cuando la F no es significativa, no quedan variables o la correlación es visiblemente baja (el programa avisa y el usuario decide).
8. Estimación numérica del modelo obtenido.
9. Obtención de los modelos no lineales (exponencial y potencial) con las mismas variables.
10. Comparación de modelos lineal, exponencial y potencial por R² (y r) **en la escala original de Y**.

## Decisiones de diseño

- **Entrada de datos:** una matriz donde cada fila es una observación; la primera columna es Y y las demás son X. Número de variables flexible.
- **Estimación reutilizada:** el modelo se calcula una vez y los submódulos lo reutilizan; si cambian los datos, se recalcula.
- **Salida estilo formulario:** H0/H1, α, estadístico, criterio de rechazo, valor calculado, p-valor y decisión. Modo *examen* (corto) y modo *estudio* (con pasos intermedios).
- **Sección 3.7:** se usan **n − 2** grados de libertad, según el docente (se define en una sola línea del código para poder cambiarlo).
- **Modelos no lineales:** requieren y > 0 (y x > 0 en el potencial); el programa lo valida.
- **Validaciones:** datos insuficientes, Sxx = 0, matriz singular, α fuera de (0,1), grados de libertad ≤ 0.

## Estructura prevista del repositorio

```
hp-prime-econometria/
├── README.md
├── src/
│   ├── nucleo.txt          (funciones comunes: sumas, matrices, distribuciones, formato)
│   ├── tema1.txt           (regresión simple)
│   ├── tema2.txt           (regresión múltiple)
│   ├── tema4.txt           (correlación)
│   └── menu.txt            (menú principal)
├── docs/
│   ├── diseno.md           (decisiones y dudas abiertas)
│   └── formulario/         (ver nota sobre derechos)
└── tests/
    └── casos_prueba.md     (datos de ejemplo y resultados esperados)
```

El código se guarda como texto plano (`.txt`) para ver cambios en GitHub y se copia al emulador; el `.hpprgm` se genera desde el emulador o el Connectivity Kit.

## Hoja de ruta

- [x] **Fase 0:** prototipo de interfaz (menú, captura y guardado de la matriz de datos)
- [x] **Fase 1:** núcleo común (sumas, matrices, p-valores, valores críticos)
- [ ] **Fase 2:** Tema 1 – regresión simple
- [ ] **Fase 3:** Tema 2 – regresión múltiple
- [ ] **Fase 4:** Tema 4 – correlación y asistente "Mejor modelo"
- [ ] **Fase 5:** integración, pulido y documentación
- [ ] **Después:** Tema 5 y Tema 3

## Instalación (cuando haya código)

1. Instala el **HP Prime Virtual Calculator** o el **HP Connectivity Kit**.
2. Abre el catálogo de programas (`Shift` + `1`) y crea un programa nuevo por cada archivo de `src/`, pegando su contenido.
3. Pulsa **Check** para revisar y ejecuta `MENU()` desde la pantalla Home.
4. Para pasarlo a la calculadora física, transfiere los programas con el Connectivity Kit.

## Pruebas

Cada módulo se valida con:

- Ejercicios resueltos de clase (datos y respuestas en `tests/casos_prueba.md`).
- Valores de referencia calculados de forma independiente (por ejemplo con Python).
- Verificaciones internas (regresión simple por Sxy/Sxx y por matrices debe dar lo mismo).

## Limitaciones conocidas

- Pantalla pequeña (320 × 240): las tablas se dividen en varias pantallas.
- La calculadora usa valores exactos de t, F y Z; en clase se usan tablas, así que en casos límite la decisión podría diferir por redondeo.
- Escribir muchos datos en la calculadora es lento; se recomienda capturarlos en el emulador y transferirlos.

## Nota sobre el formulario

El formulario de la materia es material de su autor (Univ. Jhonatan Pally Cotaña). Si el repositorio es público, **no lo subas sin su permiso**; usa un repositorio privado o añade la carpeta `docs/formulario/` al `.gitignore`.

## Uso responsable

Herramienta de estudio y verificación. Usa la calculadora en evaluaciones solo si el docente lo permite.

## Autor

*SOFTWARE: Univ. Barrionuevo Delgado Angel*
*FORMULARIO : Univ, Jhonatan Pally* 
Materia SIS-3540, Modelos Econométricos.

## Licencia

*MIT*
