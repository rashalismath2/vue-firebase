<template>
  <form  class="form-inline ml-2">
    <div class="form-group p-2">
      <input v-model.lazy="name" type="text" name="name" class="form-control-plaintext p-1" placeholder="Name.." id="name" />
    </div>
    <div class="form-group mx-sm-3 p-2">
        <input v-model.lazy="city"  type="text" name="city" class="form-control-plaintext p-1" placeholder="City.." id="city" />
    </div>
    <button v-on:click.prevent="save" type="submit"  class="btn  btn-primary p-2 m-auto">Add</button>
  </form>
</template>

<script>
export default {
    methods: {
        save(){
            if(this.city!="" && this.name!=""){
                this.$emit("form-data",{
                    name:this.name,
                    city:this.city
                });
                this.name=""
                this.city=""
            }
        }
    },
    data() {
        return {
            name:"",
            city:""
        }
    },
}
</script>


<style lang="scss" scoped>
    form{
        background-color: floralwhite;

        div input{
            background-color: #deb887
        }
        
    }
    button{
        background-color :#827968;
        border-color:white;
    }
</style>