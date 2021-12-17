<template>
<div class="bg-gray-200 flex content-center justify-center items-center h-full">
  <div class="w-full max-w-lg">
    <div class="bg-white shadow-md rounded-2xl px-8 py-8 mb-4">
      <h1 class="text-2xl font-bold text-gray-800 mb-6" v-if="mode == 'login'">Connexion</h1>
      <h1 class="text-2xl font-bold text-gray-800 mb-6" v-else>Se connecter</h1>
      <p class="text-base text-stone-500" v-if="mode == 'login'">Tu n'as pas encore de compte ? <span class="text-sky-600 underline cursor-pointer" @click="switchToCreateAccount()">Créer un compte</span></p>
      <p class="text-base text-stone-500" v-else>Tu as déjà un compte ?  <span class="text-sky-600 underline cursor-pointer" @click="switchToLogin()">Se connecter</span></p>

      <form action="" class="mt-4">
        <div class="mb-6">
          <input v-model='email' class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Adresse mail"/>
        </div>

        <div class="flex flex-wrap -mx-3 mb-6" v-if="mode == 'create'">
          <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
            <input v-model="name.prenom" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white" type="text" placeholder="Prenom">
          </div>
          <div class="w-full md:w-1/2 px-3">
            <input v-model="name.nom" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Nom">
          </div>
        </div>

        <div class="mb-6">
          <input v-model='password' class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="password" placeholder="Mot de passe"/>
        </div>

        <p class="text-red-500 text-xs italic mb-6" v-if="mode == 'login'">Adresse mail et/ou mot de passe invalide</p>
        <p class="text-red-500 text-xs italic mb-6" v-if="mode == 'create'">Adresse mail déjà utilisée</p>

        <div class="flex items-center justify-center">
          <button 
            v-if="mode == 'login'"
            @click="login()"
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            :class="{'cursor-not-allowed': !validateFields}"
            type="button">
            Connexion
          </button>
          <button 
            v-else
            @click="createAccount()"
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            :class="{'cursor-not-allowed': !validateFields}"
            type="button">
            Créer mon compte
          </button>
        </div>
      </form>
    </div>
  </div>
</div>
</template>

<script>

  export default {
    name: 'Login',
    data() {
      return {
        mode: 'login',
        email: '',
        username: '',
        name: {
          nom: '',
          prenom: '',
        },
        password: '',
      }
    },
    computed: {
      validateFields() {
        if(this.mode = 'create') {
          if (this.email != "" && this.name.prenom != "" && this.name.nom != "" && this.password != "") {
            return true;
          } else {
            return false;
          }
        } else {
           if (this.email != "" && this.password != "") {
             return true;
          } else {
            return false;
          }
        }
      }
    },
    methods: {
      switchToCreateAccount() {
        this.mode = 'create';
      },
      switchToLogin() {
        this.mode = 'login';
      },
      login() {

      },
      createAccount() {
        console.log(this.email, this.name.prenom, this.name.nom, this.password);
        this.$store.dispatch('createAccount', {email: this.email, username: this.name.prenom, password: this.password, prenom: this.name.prenom, nom: this.name.nom})
      }
    }
  }
</script>
