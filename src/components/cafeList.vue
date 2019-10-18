<template>
    <div>
        <ul class="pl-2">
            <li class="mb-2" v-for="cafe in cafeList" v-bind:key="cafe.id">
                <div class="p-2 "> 
                    <h3 class="d-flex">{{cafe.name}}<span id="cross" class="ml-auto" v-on:click="deleteItem(cafe.id)">x</span></h3>
                    <p class="mb-0">{{cafe.city}}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {    
    props:{
        cafeList:{
            type:Array,
            required:true
        }
    },
    methods: {
        deleteItem(id){
            this.$emit("delete-request",id);
        }
    },
}
</script>

<style lang="scss" scoped>

    #cross:hover{
        cursor:default;
        color: red
    }

    ul{
        list-style-type: none;

        li{
            background-color: floralwhite;

        }
    }

</style>