# Archivo de Decisiones - TP01 Git Básico - Delfina

Este documento registra las decisiones técnicas y estratégicas tomadas durante el desarrollo del trabajo práctico.

## 1. Configuración del Entorno y Repositorio

- **Flujo de Trabajo Inicial:** Se optó por realizar un **Fork** del repositorio base en lugar de un clon directo. Esta decisión simula un entorno de trabajo colaborativo estándar (como en el open-source), donde no se tiene acceso de escritura directo al repositorio original. Permite trabajar en una copia personal de forma aislada y proponer cambios mediante Pull Requests.
- **Identidad en Git:** Se comprobo la identidad local (`user.name` y `user.email`) para asegurar la correcta autoría de los commits. Esto es un pilar fundamental para la trazabilidad en cualquier proyecto.

## 2. Desarrollo de Nueva Funcionalidad (feature/mejorar-saludo)

- **Estrategia de Ramas:** Se creó una rama `feature/mejorar-saludo` a partir de `main`. Esta práctica es esencial para aislar el desarrollo de nuevas funcionalidades, evitando desestabilizar la rama principal (`main`), que se considera código en producción. El nombre sigue la convención `tipo/descripcion-corta`.

- **Commits Atómicos:** El trabajo se dividió en dos commits:
    1.  `feat: Permite personalizar el saludo...`: Modifica la lógica de la aplicación.
    2.  `feat: Actualiza archivo de datos...`: Actualiza la información relacionada.

Esta separación asegura que cada commit tenga una única responsabilidad, lo que facilita la revisión del código, la identificación de errores (`git bisect`) y la posibilidad de revertir cambios específicos sin afectar otros. Los mensajes siguen la convención de "Conventional Commits" para aportar claridad semántica al historial.

## 3. Corrección de Error Urgente (Hotfix)

- **Simulación y Aislamiento:** Se simuló un error directamente en `main` para replicar un escenario de producción. Para corregirlo, se creó una rama `hotfix/corregir-readme` a partir de `main`. Esta estrategia (Git Flow) permite desarrollar una solución urgente sin interferir con la rama `main` ni con las ramas `feature` en curso.

- **Estrategia de Integración:**
    - **Hacia `main`:** Se utilizó `git merge`. El merge es ideal en este caso porque es una operación no destructiva que integra el historial completo del hotfix en la rama principal, manteniendo una trazabilidad clara y explícita de la corrección.
    - **Hacia `feature/mejorar-saludo`:** También se usó `git merge` desde `main` hacia la rama de feature. Esto asegura que la rama de desarrollo se mantenga sincronizada con la base de código de producción, incorporando correcciones críticas y previniendo futuros conflictos de integración. Se prefirió `merge` sobre `cherry-pick` para traer no solo este fix, sino cualquier otro cambio que pudiera haber en `main`.

- **Limpieza:** Una vez integrado, la rama `hotfix` fue eliminada tanto localmente como en el repositorio remoto, ya que cumplió su propósito y ya no es necesaria.


## 4. Integración mediante Pull Request (PR)

- **Proceso:** La rama `feature/mejorar-saludo` se integró a `main` a través de un Pull Request en GitHub. Este mecanismo es estándar en flujos de trabajo colaborativos, ya que formaliza la propuesta de cambio y abre un espacio para la revisión de código (`code review`), asegurando la calidad antes de que el código llegue a la rama principal.

- **Merge y Limpieza:** Se utilizó la estrategia de "Merge Commit" por defecto de GitHub. Tras la fusión exitosa, la rama `feature/mejorar-saludo` fue eliminada tanto en el repositorio remoto como en el local para mantener el repositorio limpio y evitar la acumulación de ramas obsoletas.

## 5. Creación de una Versión Etiquetada (Tagging)

- **Convención de Versionado:** Se utilizó el versionado semántico (SemVer) para nombrar la etiqueta. Se creó el tag `v1.0` para marcar la primera versión estable del proyecto. La `v` inicial es una convención común para denotar "versión".

- **Tipo de Tag:** Se optó por un **tag anotado** (`git tag -a`) en lugar de uno ligero. Los tags anotados son tratados como objetos completos en la base de datos de Git y almacenan metadatos adicionales (autor, fecha, mensaje), lo cual es crucial para la trazabilidad de los lanzamientos oficiales.

- **Publicación:** El tag fue subido explícitamente al repositorio remoto (`git push origin v1.0`), ya que los tags no se transfieren con un `git push` estándar. Esto hace que la versión sea visible y accesible para todo el equipo.

## 6. Conclusiones y Buenas Prácticas

- **Flujo de Trabajo:** El flujo seguido (una mezcla de GitHub Flow y conceptos de Git Flow) demostró ser eficaz para manejar desarrollo paralelo (feature) y correcciones urgentes (hotfix) sin conflictos.
- **Trazabilidad:** El uso de ramas descriptivas, commits atómicos con mensajes convencionales y un archivo de decisiones permite reconstruir la historia del proyecto y entender el "porqué" de cada cambio.
- **Calidad en un Equipo Real:** Para asegurar la calidad, se implementarían Pull Requests obligatorios con revisiones de al menos un colega, integración continua (CI) para correr pruebas automáticas en cada PR, y políticas de protección de la rama `main` para evitar pushes directos.