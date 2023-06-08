# TaskMaster Test
## Creating a project

Se creo la prueba FRONTEND-TECNICO con el framework Svelte y la herramienta de compilacion VITE teniendo conexion en backend a SUPABASE en donde se creo una tabla con los requerimientos solicitados



## Desarrollo

Se instalaron las dependencias mediante `npm install` (or `pnpm install`), iniciando un servidor de desarrollo:
npm run dev


## Dependences
Se instalaron dependencias y librerias como bootstrap@5.3.0 para el maquetado y svelte-fa@3.0.4 para iconos

## Flujo
Se crearon los endpoints ***getAllTodos***, ***addNewTodo***, ***updateTodo***, ***deleteTodo***, para el manejo de la data, esto en archivo ***App.svelte***

Se creo el componente ***Todo.svelte*** en la carpeta **component/Todo.svelte** para la renderizacion del mismo
Se creo el archivo **.env** con las variables de entorno para la conexion a la API de la tabla creada en SUPABASE


