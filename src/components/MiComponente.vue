<template>
    <div>
        <ul>
            <li v-for="(user,index) in users" :key="index+lastName+name">{{user.name}} {{user.lastName}}</li>
        </ul>
        <button v-on:click="isHidden = !isHidden">Add Componente</button>
        <div v-if="!isHidden" >
            <input v-model="newUserName">
            <br>
            <input v-model="newUserlName">
            <br>
            <button @click="addUser" class="button" v-on:click="isHidden=true">Icono</button>
        </div>
    </div>
     
</template>

<script>
export default {
    name: "MiComponente",
    data(){
        return{
            isHidden:true,
            newUserName:"",
            newUserlName:"",
            users:[
                {
                    name:"Luis",
                    lastName:"Cortez",
                    imageUrl:""
                },
                {
                    name:"Eduardo",
                    lastName:"Murillo",
                    imageUrl:""
                }
                ,{
                    name:"Vale",
                    lastName:"Cortez",
                    imageUrl:""
                }
                ]
        }
        
    },
    methods:{
        addUser(){
            if(this.newUserName !== '' || this.newUserlName !==''){
                this.users.push({
                    name:this.newUserName,
                    lastName:this.newUserlName
                })
                this.newUserName = ""
                this.newUserlName = ""
            }
        }
    }
}
</script>
<style>
.miC{
    background-color: red;
}

.users{
    border-top:1px solid #ddd;
}

.name{
    float: left;
   
}

.lastname{
    float: right;
    
}
</style>