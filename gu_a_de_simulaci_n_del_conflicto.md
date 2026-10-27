# Guía Práctica: Simulación de Conflicto en Git

Este repositorio es parte del caso de estudio de la clase. El objetivo es simular un entorno de trabajo colaborativo donde dos desarrolladores (Ana y Carlos) editan la misma línea de código, generando un conflicto de fusión (Merge Conflict) que deberán resolver.

---

## 🛠️ Paso 0: Preparación (Líder del equipo / Profesor)
1. Crea un repositorio en GitHub.
2. Sube estos archivos iniciales (`index.html` y `README.md`) a la rama `main`.
3. Pide a Ana y Carlos que clonen el repositorio en sus computadoras:
   ```bash
   git clone <url-del-repositorio>
   cd <nombre-del-repo>
   ```

---

## 👩‍💻 Paso 1: El turno de Ana
Ana debe añadir su servicio al portafolio y enviarlo al servidor.

1. **Crear una nueva rama y cambiar a ella:**
   ```bash
   git switch -c rama-ana
   ```
2. **Modificar el código:** Abre `index.html`. En la sección de servicios (cerca de la línea 45), añade:
   `<li>Consultoría IT</li>`
3. **Guardar los cambios:**
   ```bash
   git add index.html
   git commit -m "Añade servicio de Consultoría IT"
   ```
4. **Subir la rama al repositorio remoto:**
   ```bash
   git push -u origin rama-ana
   ```
5. **En GitHub:** Ana (o el líder) debe crear un *Pull Request* desde `rama-ana` hacia `main` y aceptarlo (Merge). **Ahora la rama principal en la nube tiene los cambios de Ana, pero Carlos aún no lo sabe.**

---

## 👨‍💻 Paso 2: El turno de Carlos
Carlos comienza a trabajar desde su código base antiguo, sin descargar los cambios que acaba de hacer Ana.

1. **Crear su propia rama (estando en main):**
   ```bash
   git switch -c rama-carlos
   ```
2. **Modificar el código:** Abre `index.html`. En la *misma línea exacta* donde Ana añadió su código (línea 45), añade:
   `<li>Asesoría Legal</li>`
3. **Guardar los cambios:**
   ```bash
   git add index.html
   git commit -m "Añade servicio de Asesoría Legal"
   ```

---

## 💥 Paso 3: El Conflicto
Carlos intenta actualizar su código local integrando la rama principal (que ya tiene lo de Ana).

1. Carlos actualiza su repositorio local con la información remota:
   ```bash
   git fetch origin
   ```
2. Carlos intenta fusionar la rama `main` del remoto hacia su rama actual (`rama-carlos`) para estar al día antes de subir su código:
   ```bash
   git pull origin main
   ```
3. **¡BOOM! Git mostrará un error:** 
   `CONFLICT (content): Merge conflict in index.html`

---

## 🤝 Paso 4: La Solución Conjunta
Carlos debe resolver el conflicto manualmente.

1. **Abrir el editor (VS Code recomendando):**
   Carlos abre `index.html` y verá unas marcas insertadas por Git:
   ```html
   <<<<<<< HEAD
   <li>Asesoría Legal</li>
   =======
   <li>Consultoría IT</li>
   >>>>>>> branch 'main' of origin
   ```
2. **Editar:** Carlos borra las marcas (`<<<<<<<`, `=======`, `>>>>>>>`) y acomoda el código para que *ambos* servicios se mantengan en la lista.
3. **Marcar como resuelto:**
   ```bash
   git add index.html
   ```
4. **Completar la fusión:**
   ```bash
   git commit -m "Resuelve conflicto conservando ambos servicios"
   ```
5. **Subir los cambios finales:**
   ```bash
   git push -u origin rama-carlos
   ```
*Finalmente, Carlos puede abrir su Pull Request en GitHub, ¡y ya no habrá conflictos!*