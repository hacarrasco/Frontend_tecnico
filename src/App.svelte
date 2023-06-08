<script>
  import supabase from "../db";
  import { onMount } from "svelte";
  import Todo from "./component/Todo.svelte";

  let todos = [];
  let newTodo = "";

  onMount(async () => {
    await getAllTodos();
  });

  const getAllTodos = async () => {
    try {
      let { data, error } = await supabase.from("todos").select("*");
      todos = data;
    } catch (error) {
      // @ts-ignore
      console.log(err);
    }
  };

  const addNewTodo = async () => {
    try {
      const { data, error } = await supabase
        .from("todos")
        .insert([{ titlem: newTodo }]);
      await getAllTodos();
      newTodo = "";
    } catch (error) {
      // @ts-ignore
      console.log(err);
    }
  };

  const updateTodo = async (todo) => {
    try {
      const { data, error } = await supabase
        .from("todos")
        .update({ titlem: todo.titlem, state: todo.state })
        .eq("id", todo.id);
      await getAllTodos();
    } catch (error) {
      // @ts-ignore
      console.log(err);
    }
  };

  const deleteTodo = async (todo) => {
    try {
      const { data, error } = await supabase
        .from("todos")
        .delete()
        .eq("id", todo.id);
      await getAllTodos();
    } catch (error) {
      // @ts-ignore
      console.log(err);
    }
  };

  const handleKeyPress = (event) => {
    if (event.key === "Enter" && newTodo !== "") {
      addNewTodo();
    }
  };
</script>

<div class="col-lg-8 col-sm-12" style="margin: 200px 0 0 0px;">
  <div class="responsive">
    <div class="card" style="background-color: rgb(31, 41, 55);">
      <div class="card-body" style="height: auto;">
        <h3 style="color: #fff; padding-bottom:20px">TaskMaster</h3>
        <div style="display: flex;">
          <input
            class="col-md-10 col-sm-2"
            placeholder="Add a new todo..."
            style="background: rgb(55, 65, 81); color:#fff"
            type="text"
            bind:value={newTodo}
          />
          <button class="btn btn-primary col-md-2" on:click={() => addNewTodo()}
            >Add</button
          >
        </div>
        <br />

        {#each todos as todo}
          <Todo {todo} {updateTodo} {deleteTodo} />
        {:else}
          <p>No hay tareas</p>
        {/each}
        <div class="col-md-12" style="display: inline-flex;">
          <p>Total Todos: {todos.length} |</p>
          <p style="margin-left:5px ;">Completed Todos: 0</p>
        </div>

        <p style="color:#fff; font-style:italic">
          "Believe you can and you're halfway there." - Theodore Roosevelt
        </p>
      </div>
    </div>
  </div>
</div>

<svelte:window on:keypress={handleKeyPress} />

<style>
  p {
    color: #fff;
  }

  @media screen and (min-width:1000px){
    .responsive {
      margin-left: 350px;
    }
  }

  @media screen and (max-width: 400px) {
    .responsive {
      margin-left: 50px;
    }
  }
</style>
