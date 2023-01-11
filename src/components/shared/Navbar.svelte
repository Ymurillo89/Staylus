<script lang="ts">
    import { Router, Link, Route } from "svelte-routing";
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger,Button } from 'flowbite-svelte'
    import Home from "../external/Home.svelte";
    import Login from "../external/Login.svelte";    
    import NavInternal from "../internal/NavInternal.svelte";
    
    import { viewNavExternal } from "../../store/store";
    import { onMount } from "svelte";
  import MainSettingSchedule from "../internal/settingSchedule/MainSettingSchedule.svelte";
  import Report from "../internal/reports/Report.svelte";
  

    let urls=[{name:"Home",url:"Home"},]
    onMount(async () => {
		  viewNavExternal.update(()=>urls)
	  });  
 
    let mainMenu:boolean=false;
    function mainMenuBar(){
        mainMenu= true;
    }
  
    function closeMenuBurger(){    
        mainMenu=false;
    }


</script>

<Router>
  
  <Navbar let:hidden let:toggle >
    <NavBrand href="/">
        <img
          src="https://flowbite.com/docs/images/logo.svg"
          class="mr-3 h-6 sm:h-9"
          alt="Flowbite Logo"
        />
        <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">
          Staylus
        </span>
      </NavBrand >
      <div class="flex md:order-2" >
        <Link   class="inline-block rounded bg-indigo-600 px-4 py-2 text-sm font-medium text-white transition hover:scale-110 hover:shadow-xl focus:outline-none focus:ring active:bg-indigo-500"
              to="Login">
              <i class="fas fa-user">

              </i>      
        </Link>
        <NavHamburger on:click={toggle} />
      </div>
      <NavUl {hidden} class="order-1">
        {#each $viewNavExternal as lins}
           <!-- content here -->
           <NavLi ><Link to="{lins.url}">{lins.name}</Link></NavLi>    
        {/each}
    
      </NavUl>
  </Navbar>  
   

    <Route path="Home" component="{Home}"/>
    <Route path="Login" component="{Login}"/>
    <Route path="Internal" component="{NavInternal}"/>
    <Route path="mainSettingSchedule" component="{MainSettingSchedule}"/>      
        <Route path="report" component="{Report}"/>    
   
    <Route path="/"><Home /></Route>

</Router>


  