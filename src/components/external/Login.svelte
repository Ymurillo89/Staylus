<script lang="ts">  
    import { navigate } from "svelte-routing";
    import type { IGetUser } from '../../models/interfaces';

    import { onMount } from "svelte";
    import { viewNavExternal } from "../../store/store";
  
    onMount(async () => {
      //viewNavExternal.update(()=>0)
    });

    let number:number =0
    let user:string="";
    let password:string="";

    let dataUser:IGetUser[]=[];
    let alert:boolean = false

    

    //Verificamos que las credenciales sean correctas y enviamos a la página correspondiente

    async function getLogin(){
   
      alert= false;

      if(user!="" && password !=""){
        const rawResponse = await fetch(`https://andresmu91.bsite.net/api/LoginCtrl/Login/${user}/${password}`, 
        {
          method: 'GET',  
          headers: {
          'Content-Type': 'application/json;charset=utf-8'
          },          
        });

        dataUser= await rawResponse.json();                

        if(dataUser.length==0){
          alert=true
        }else{

          dataUser.forEach(element => {
          localStorage.setItem("Staff",element.idRowStaff.toString())
          localStorage.setItem("Location",element.idRowLocation.toString())
          localStorage.setItem("IdRowStore",element.idRowStore.toString())
          localStorage.setItem("User",element.usser)
          });

          //Ruteamos hacia otra pestaña          
          navigate("Internal")
        }

        

      }else{
        alert=true
      }
       
    }  
  
</script>

<section class="relative flex flex-wrap lg:h-screen lg:items-center">
    <div class="w-full px-4 py-12 sm:px-6 sm:py-16 lg:w-1/2 lg:px-8 lg:py-24">
      <div class="mx-auto max-w-lg text-center">
        <h1 class="text-2xl text-white font-bold sm:text-3xl ">Una excelente oferta</h1>
  
        <p class="mt-4 text-gray-500">
          Para tener el control de tú negocio
        </p>
      </div>
  
      <form  class="mx-auto mt-8 mb-0 max-w-md space-y-4">
        <div>
          <label for="email" class="sr-only">Usuario</label>
  
          <div class="relative">
            <input
              bind:value={user}
              type="text"
              class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Usuario"
            />
  
            <span class="absolute inset-y-0 right-4 inline-flex items-center">
             <!--  <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-gray-400"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"
                />
              </svg> -->
            </span>
          </div>
        </div>
  
        <div>
          <label for="password" class="sr-only">Password</label>
          <div class="relative">
            <input
              bind:value={password}
              type="password"
              class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Contraseña "
            />
  
            <span class="absolute inset-y-0 right-4 inline-flex items-center">
             <!--  <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-gray-400"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                />
              </svg> -->
            </span>
          </div>
        </div>
  
        {#if alert}
          <p class="text-sm text-gray-500 text-center">
             usuario o contraseña incorrectos
          </p>
        {/if}
        
      </form>
      <div class="flex items-center justify-center mt-2"> 
        <button    
          on:click={getLogin}        
          type="submit"
          class="inline-block rounded-lg bg-blue-500 px-5 py-3 text-sm font-medium text-white">
          Ingresar
        </button>
      </div>
    </div>
  
    <div class="relative h-64 w-full sm:h-96 lg:h-full lg:w-1/2">
      <img
        alt="Welcome"
        src="https://images.unsplash.com/photo-1630450202872-e0829c9d6172?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80"
        class="absolute inset-0 h-full w-full object-cover"
      />
    </div>
  </section>