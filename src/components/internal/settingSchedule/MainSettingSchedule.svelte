<script lang="ts">
    import { Tabs, TabItem } from 'flowbite-svelte';
    import type { IGetHour} from '../../../models/interfaces'   
  </script>  

  <Tabs style="underline" class="flex justify-center container m-auto ">
    <TabItem  open>
      <div slot="title">
            <i class="fas fa-user-clock fa-2x"></i>       
            <div>
              Configuración     
            </div> 
            <div>
              Disponibilidad     
            </div> 
      </div>    

      <div class="container m-auto">
    <!--      <Timetable />    -->    
      </div>
      
    </TabItem>

    <TabItem >
      <div slot="title">
          <i class="fas fa-calendar-week fa-2x"></i>    
            <div>
              Fechas
            </div> 
            <div>
              Disponibilidad     
            </div> 
      </div>    

      <div class="container m-auto">
      <!--    <DateAvailable />    -->    
      </div>
      
    </TabItem>

    <TabItem >
      <div slot="title" class="">
        <i class="fas fa-clock fa-2x"></i>
        <div>
          Citas 
        </div>
        <div>
          Ocupadas
        </div>
      </div>
      <p class="text-sm text-gray-500 dark:text-gray-400"><b>Dashboard:</b> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
    </TabItem>  
   
  </Tabs>


  