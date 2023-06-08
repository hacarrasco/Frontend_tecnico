<script>
    export let todo, updateTodo, deleteTodo;
    // @ts-ignore
    import Fa from "svelte-fa/src/fa.svelte";
  // @ts-ignore
  import { faTrashCan, faCheck } from '@fortawesome/free-solid-svg-icons'
  
    export let itsComplete = false;
  
    const todoComplete = (todo) => {
     if(todo.state !== itsComplete) {
      itsComplete = !itsComplete
     } 
      }
    
  </script>
  
  <div>
    <div class="todos">
      <input
        class={itsComplete ? 'active' : ''}
        style="background: rgb(55, 65, 81); border-color:transparent; color:#fff; border-radius: 3px"
        type="text"
        value={todo.titlem}
        on:input={(e) => {
          todo.titlem = e.currentTarget.value;
          updateTodo(todo);
        }}
        disabled
      />
  
      <button class="btn1"  type="button"
         on:click={todoComplete}
      >
        <Fa icon={faCheck}/>
      </button>
  
  
      <button class="btn" type="button"
        on:click={() => deleteTodo(todo)}>
        <Fa icon={faTrashCan} /> 
      </button>
    </div>
    <br />
  </div>
  
  <style>
    
    .todos {
      width: 400px;
      background: rgb(55, 65, 81);
      display: flex;
      margin-bottom: 0.25em;
      justify-content: center;
      gap: 15px;
      margin-left: 50px;
    }
    .btn1{
      background-color: rgb(55, 65, 81);
      color: green;
      border: none;
    }
    .btn{
      background-color: rgb(55, 65, 81);
      color: red;
      border:none
    }
  
    .active{
      opacity:0.5;
      text-decoration: line-through;
    }
  </style>
  