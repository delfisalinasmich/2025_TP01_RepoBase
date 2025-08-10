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