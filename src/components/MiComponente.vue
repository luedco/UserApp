<template>
  <div class="user-grid-displayer">
    <div class="display-user" v-if="!displayHidden">
      <div class="img-container">
        <img :src="displayImage" alt="no hay:c" />
      </div>

      <p>Nombre: {{displayName}}</p>
      <p>Apellido: {{displayLastName}}</p>
    </div>
    <div
      class="user-container hex"
      v-for="(user,index) in users"
      :key="index"
      @click="displayUser(user,index)"
      v-on:click="displayHidden = !displayHidden"
    >
      <a v-if="users.length===0">No hay users</a>
      <a class="btn-user">{{user.name}} {{user.lastName}}</a>
    </div>

    <button v-on:click="isHidden = !isHidden">Add Componente</button>
    <div v-if="!isHidden">
      <input type="file" @change="onFileChange($event)"/>
      <br />
      <input v-model="newUserName" />
      <br />
      <input v-model="newUserlName" />
      <br />
      <button @click="addUser()" class="button" v-on:click="isHidden=true">Icono</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MiComponente",
  data() {
    return {
      isHidden: true,
      newUserName: "",
      newUserlName: "",
      newUserUrl: "",
      displayName: "",
      displayLastName: "",
      displayImage: "",
      displayHidden: true,
      users: [
        {
          name: "Luis",
          lastName: "Cortez",
          imageUrl: "",
        },
        {
          name: "Eduardo",
          lastName: "Murillo",
          imageUrl: "",
        },
        {
          name: "Vale",
          lastName: "Cortez",
          imageUrl: "",
        },
      ],
    };
  },
  methods: {
    addUser() {
       let index=this.users.length-1;
      console.log("AddUser"+index)
      if (this.newUserName !== "" || this.newUserlName !== "") {
        /**
         * Esta funcion ya no crea usuarios, solo toma el indice y agrega los campos que faltan
         */
        /*
        this.users.push({
          name: this.newUserName,
          lastName: this.newUserlName,
        });*/
        
        //AgregarNuevosCampos

        this.users[index].name =this.newUserName
        this.users[index].lastName =this.newUserlName
        this.newUserName = "";
        this.newUserlName = "";
      }
      
    },
    displayUser(user, index) {
      console.log(
        index + " " + user.name + " " + user.lastName + " "
      );
      this.displayName = user.name;
      this.displayLastName = user.lastName;
      this.displayImage = user.imageUrl;
    },
    onFileChange(e){
      /**
       * Como esta funcion se manda a llamar antes de agregar al usuario actual 
       * en la lista de users no existe todavía
       * length devuelve 3 (originales)
       */
      /**
       * Objetivo: crear el usuario aqui y solo agregar los campos faltantes en addUser()
       */

      this.users.push({
        name:"",
        lastName:"",
        imageUrl:""
      })
      let index=this.users.length;
      console.log("FileChange"+index)
      var files = e.target.files ||  e.dataTransfer.files
      if (!files.length) {return;}
      this.createImage(this.users[index-1], files[0]);
    },
    createImage(item, file) {
      var image = new Image();
      var reader = new FileReader();
      console.log(image);
      reader.onload = (e) => {
        item.imageUrl = e.target.result;
      };
      reader.readAsDataURL(file);
    },
  },
};
</script>
<style>
.miC {
  background-color: red;
}

.users {
  border-top: 1px solid #ddd;
}

.user-grid-displayer {
  display: grid;
}
.user-container {
  background: blue;

  color: black;
}
.btn-user {
  text-decoration: none;
}

.hex {
  height: 45px;
  width: 45px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  border: red;
  border-width: 2px;
}
.img-container {
  display: grid;
  height: 167px;
  width: 191px;
}
.img-item {
  height: 149px;
  width: 172px;
}
</style>