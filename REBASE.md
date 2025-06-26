# Documentación de la tarea 7: Limpieza de commits con "git rebase -i"

## Fecha: 26 de junio de 2025

### 1. Objetivo de la tarea
 El objetivo principal de esta tarea fue aprender a utilizar la herramienta `git rebase -i` (rebase interactivo) 
 para limpiar y organizar el historial de commits de un repositorio. 
 Esto incluye cambiar mensajes de commits, fusionar (squash/fixup) commits pequeños o redundantes, 
 y, finalmente, forzar la actualización del historial en el repositorio remoto.

### 2. Simulación del historial desordenado
 Para esta práctica, se creó un nuevo repositorio (PRUEBAS-TAREA- 7Y8) y se generaron intencionalmente una serie de commits con mensajes poco claros y cambios pequeños para simular un historial típico que requeriría limpieza.

 Historial de commits previo a `git rebase -i`

    bec6602 Lo arregle
    cce1c69 Actualizacion de cosas
    a3e8ed0 Cambios
    920cb4b Arreglos
   108c2cf Initial commit
    
 Los archivos que afentan son: `README.md`, `cosa.txt`, `bug7.txt`.

### 3. Proceso de Limpieza con `git rebase -i`

Se utilizó `git rebase -i` para modificar los últimos 4 commits, fusionándolos y aclarando sus mensajes.

 * 3.1. Inicio del Rebase Interactivo

 Se identificó el commit inicial (`108c2cf Initial commit`) como el punto de inicio para el rebase.

  Para ello se utilizó:
    
    `git rebase -i 108c2cf`

    
 * 3.2. Edición del Archivo de Rebase

 El editor de texto se abrió automáticamente con la lista de commits. En este caso se modificaron las palabras clave `pick` por `reword` o `fixup` según la intención:

 El resultado fue el siguiente:
    
    reword 920cb4b Arreglos
    fixup 3ae8ed0 Cambios
    fixup cce1c69 Actualizacion de cosas
    reword bec6602 arreglo
    

 * 3.3. Edición de Mensajes de Commits (`reword`)

 Una vez guardado y seccrado el edictor de texto anterior Git abrió otro editor para cada commit marcado con `reword`:

   Commit 1 (anteriormente "Arreglos"):
    * Mensaje anterior: "Arreglos"
    * Nuevo mensaje: "primer commit en README.md"

   Commit 2 (anteriormente "arreglo", fusionando "actualizacion de cosas" y "cambios"):
    * Mensajes anteriores: "Cambios", "Actualizacion de cosas", "Lo arregle"
    * Nuevo mensaje consolidado:"solucionado el problema de bug7"

 * 3.4. Confirmación del Historial Limpio

 Después de completar los pasos del rebase, se verificó el nuevo historial de commits usando:

     git log --oneline

 * Finalmente el historial final se queda así:
    
    b758e25 solucionado el problema de bug7
    5823f9d primer commit en README.md
    108c2cf Initial commit
    
### 4. Actualización del Repositorio Remoto (`git push --force`)

 Debido que el historial de commits local fue reescrito, fue necesario forzar la actualización del repositorio remoto en GitHub.

 Para ello se usó el comando:
  
    git push --force origin main
    
 Se confirmó tambien visualmente en GitHub que el historial de commits había sido actualizado para reflejar la versión limpia y organizada.
 En lugar de 5 commits solo refleja 3 commits


### 5. Lecciones Aprendidas

Esta tarea proporcionó una experiencia práctica con el comando `git rebase -i`, el cual es una herramienta fundamental para mantener un historial de commits claro y profesional.

 1. Es muy importante tener mensajes de commits claros y sencillos para facilitar la comprensión, el seguimiento de cambios y la depuración en proyectos.
 2. Se aprendió a usar `reword` para corregir mensajes, `squash` y `fixup` para combinar commits relacionados o de poca importancia en un solo commit.
 3. Se comprendió que reescribir el historial local requiere un `git push --force`, y tener una EXTREMA PRECAUCIÓN al usarlo en ramas compartidas para evitar problemas con otros colaboradores.
 4. El rebase es una herramienta muy útil para el mantenimiento del repositorio, permitiendo presentar un historial limpio y coherente para revisiones de código, lanzamientos y futuras referencias.
