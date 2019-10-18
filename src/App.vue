<template>
  <div class="col-6 m-auto pt-4" id="app">
      <div class="jumbotron jumbotron-fluid">
        <div class="container">
          <h1>Cloud cafe</h1>
          <cafe-form v-on:form-data="saveFormData($event)"></cafe-form>
          <hr class="my-4">
          <cafe-list v-on:delete-request="deleteCafeData($event)" v-bind:cafeList="cafeList"></cafe-list>
        </div>
    </div>
  </div>
</template>

<script>

  import cafelist from "./components/cafeList.vue";
  import cafeform from "./components/cafeForm.vue";

export default {
  name: 'app',
  components:{
    "cafe-list":cafelist,
    "cafe-form":cafeform
  },
  created() {
    this.getAllCafes();
    
  },
  data () {
    return {
      cafeList:[]
    }
  },
  methods: {
    deleteCafeData(id){
      db.collection("cafes").doc(id).delete().then(()=>{
        this.cafeList=this.cafeList.filter((item)=>{
          return item.id!=id;
        })
        console.log("deleted the data");
      })
      console.log(id);
    },
    saveFormData(data){
      db.collection('cafes').add({
        name:data.name,
        city:data.city
      }).then((e)=>{
        this.cafeList.push({
          city:data.city,
          name:data.name,
          id:e.id
        })
      })
    },
    getAllCafes(){
      db.collection("cafes").get()
        .then((snapshot)=>{
            snapshot.docs.forEach(doc => {
              this.cafeList.push({
                name:doc.data().name,
                city:doc.data().city,
                id:doc.id
              });
                console.log(doc.data());           
            });
      });
    }
  },
}
</script>

<style scoped lang="scss">
  #app{

    h1{
      color:white;
      font-weight: bold;
      text-transform: capitalize
    }

  }

  #app>div{
    background-color: wheat;
    border-top-right-radius: 100px;
  }

</style>
