
<template> 
  <div class="home"> 
    <div class="search py-20"> 
      <div class="w-1/2 mx-auto relative"> 
        <input 
          @keyup="checkInput()" 
          v-model="search" 
          class="w-full p-2" 
          type="text" 
          placeholder="Поиск" 
        /> 
        <i class="fa-solid fa-magnifying-glass set-search"></i> 
      </div> 
    </div> 


   

     <div 
 
    class="p-10">
    <div    
    v-for="temp of chosenObj" 
    v-bind:key="temp">
     {{temp}}
    </div>
    </div>

   
    
    
    <div 
    v-for="query of readyQuery" 
    :key="query.id"
    @click = "gotChosen(query.name)"
    > 
    {{query.name}}
    </div> 

  </div> 
</template> 
 
<script> 
import axios from "axios"; 
export default { 
  name: "HomeView", 
  data() { 
    return { 
      photos: [], 
      search: "", 
      readyQuery: [], 
      chosenObj : [],
    }; 
  }, 
  async mounted() { 
    const res = await axios.get("http://localhost:3001/todos"); 
    this.photos = res.data; 
    this.photos.forEach((item)=>{
     item.name = item.name.toLowerCase();
    });
  }, 
  methods: { 
    checkInput() { 
      this.search = this.search.toLowerCase();
      this.readyQuery = [];
      this.photos.forEach((item) => { 
        if (item.name.includes(this.search)) { 
          this.readyQuery.push(item); 
        } else { 
          console.log(item.id); 
        } 
      }); 
    }, 
  gotChosen(CObject)
  {
    if(this.chosenObj.length < 3)
    {
   this.chosenObj.push(CObject);
    }
   else
   {
    
     this.chosenObj = []
     this.chosenObj.push(CObject);
   }

  
  },
 
   onClick(){
  console.log(5555);
  }

  }, 
 
  
}; 
</script>