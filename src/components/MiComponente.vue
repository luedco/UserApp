<template>
  <div class="user-grid-displayer">
    <h1>Prueba IT</h1>
    <div class="all-user">
      
      <div class="display-user">
        <div  v-if="!displayHidden">
          <div class="img-container">
            <img :src="displayImage" alt="no hay:c" class="img-item" />
          </div>
          <p>Nombre: {{displayName}}</p>
          <p>Apellido: {{displayLastName}}</p>
        </div>
      </div>


      <div class="section2">
        <h2>Usuarios</h2>
        <div class="section2-sub">
          <div class="user-container">
            <a v-if="this.users.length===0">
              <img src="../assets/empty.svg" alt="SVG ICON" class="img-user-none"/>
            </a>
            <div
              class="hex"
              v-for="(user,index) in users"
              :key="index"
              @click="displayUser(user,index)"
              v-on:click="displayHidden = !displayHidden"
            >
              <a class="btn-user">
                <img :src="user.imageUrl" class="img-display-item" />
              </a>
            </div>
          </div>
          <button v-on:click="isHidden = !isHidden" class="btn-addUser">
            <img src="../assets/icono agregar usuario.svg" alt="SVG ICON" class="img-user-add"/>
          </button>
        </div>
      </div>

      <div class="all-addUser">
        <div v-if="!isHidden" class="sub-all-addUser">
          <input type="file" @change="onFileChange($event)" class="user-file" />
          <div class="user-input">
            <input v-model="newUserName" class="user-input-name" />
            <input v-model="newUserlName" class="user-input-lName" />
          </div>
          <button @click="addUser()" class="buttonAddUser" v-on:click="isHidden=true">Icono</button>
        </div>
      </div>


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
      users: [],
    };
  },
  methods: {
    addUser() {
      let index = this.users.length - 1;
      console.log("AddUser" + index);
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

        this.users[index].name = this.newUserName;
        this.users[index].lastName = this.newUserlName;
        this.newUserName = "";
        this.newUserlName = "";
      }
    },
    displayUser(user, index) {
      console.log(index + " " + user.name + " " + user.lastName + " ");
      this.displayName = user.name;
      this.displayLastName = user.lastName;
      this.displayImage = user.imageUrl;
    },
    onFileChange(e) {
      /**
       * Como esta funcion se manda a llamar antes de agregar al usuario actual
       * en la lista de users no existe todavía
       * length devuelve 3 (originales)
       */
      /**
       * Objetivo: crear el usuario aqui y solo agregar los campos faltantes en addUser()
       */

      this.users.push({
        name: "",
        lastName: "",
        imageUrl: "",
      });
      let index = this.users.length;
      console.log("FileChange" + index);
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) {
        return;
      }
      this.createImage(this.users[index - 1], files[0]);
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
.h1 {
  align-content: center;
}
.miC {
  background-color: red;
}

.users {
  border-top: 1px solid #ddd;
}

.user-grid-displayer {
  display: grid;
  height: 100%;
  width: 100%;
  overflow: hidden;
  justify-content: center;
  align-items: center;
  color: black;
}
.all-user {
  width: 720px;
  height: 720px;
  background: #9E96A6;
  display: flex;
  flex-direction: column;
}
.user-container {
  width: 431px;
  height: 86px;
  background: white;
  display: flex;
  margin-right: 10px;
  justify-content: center;
}

.img-user-none{
  width:99.69px;
  height: 78px;
  
}
.all-addUser {
  display: flex;
  flex-direction: row;
  padding: 100px;
}
.img-user-add{
  width:76px;
  height: 76px;
  display: flex;
  justify-content: center;
  align-content: center;
  border-radius: 75px;

}
.sub-all-addUser {
  display: flex;
  flex-direction: row;
}
.user-input {
  margin: 10px;
  align-content: space-between;
  justify-content: space-around;
    border-radius: 150px;
}

.user-input-name .user-input-lName {
  width: 300px;
  height: 40px;
  font-size: 14pt;
  border-radius: 25px;
}


.btn-user {
  text-decoration: none;
}
.btn-addUser {
  height: 86px;
  width: 86px;
  display: flex;
}
.section2-sub {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.hex {
  height: 45px;
  width: 45px;
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  border: red;
  border-width: 2px;
}

.img-item {
  height: 149px;
  width: 172px;
}
.display-user {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 288px;
}
.img-display-item {
  height: 45px;
  width: 45px;
  align-content: center;
}
.buttonAddUser{
  height: 86px;
  width: 86px;
}

</style>