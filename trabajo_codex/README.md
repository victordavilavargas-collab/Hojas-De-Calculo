# Trabajo de Excel con Codex

Esta carpeta se usa como zona de trabajo para modificar libros de Excel con Codex.

## Flujo recomendado

1. Copiar el archivo Excel original dentro de esta carpeta.
2. Codex debe trabajar sobre una copia, preservando el archivo original.
3. Guardar la versión modificada con un nombre claro y versionado.
4. Incluir, cuando corresponda, un archivo de notas con:
   - cambios realizados;
   - fórmulas modificadas;
   - hojas afectadas;
   - verificaciones ejecutadas;
   - advertencias pendientes.
5. Al terminar cada tarea:
   - revisar `git status`;
   - hacer commit con un mensaje descriptivo;
   - hacer push a `main` salvo que la tarea indique usar una rama;
   - informar el hash del commit.

## Archivos temporales

No subir archivos temporales de Excel tipo `~$*.xlsx`.
