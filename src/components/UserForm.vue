<template>
    <div class="user-form">
      <h2>Formulaire de Saisie d'Informations</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="name">Nom :</label>
          <input type="text" id="name" v-model="form.name" placeholder="Veuillez saisir votre nom" />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
  
        <div class="form-group">
          <label for="email">Email :</label>
          <input type="email" id="email" v-model="form.email" placeholder="Votre mail" />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>
  
        <div class="form-group">
          <label for="phone">Numéro de Téléphone :</label>
          <input type="text" id="phone" v-model="form.phone" placeholder="Votre numéro de télephone"  />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>
  
        <button type="submit">Soumettre</button>
  
        <div v-if="submitted" class="confirmation">
          <p>Merci ! Votre formulaire a été soumis avec succès.</p>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'UserForm',
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: ''
        },
        errors: {},
        submitted: false
      };
    },
    methods: {
      validateForm() {
        this.errors = {};
3  
        if (!this.form.name) {
          this.errors.name = 'Le nom est requis.';
        }
  
        if (!this.form.email) {
          this.errors.email = 'L\'email est requis.';
        } else if (!/\S+@\S+\.\S+/.test(this.form.email)) {
          this.errors.email = 'L\'email est invalide.';
        }
  
        if (!this.form.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!/^\d{8}$/.test(this.form.phone)) {
          this.errors.phone = 'Le numéro de téléphone doit contenir 8 chiffres.';
        }
  
        return Object.keys(this.errors).length === 0;
      },
      handleSubmit() {
        if (this.validateForm()) {
          this.submitted = true;
          // Vous pouvez également envoyer les données du formulaire ici
          console.log('Formulaire soumis :', this.form);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .user-form {
    align-items: center;
    max-width: 1200px;
    margin: auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  .user-form h2{
    color: white;
  }
  
  .form-group {
    margin-bottom: 15px;
    color: white;
    text-align: left;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .error {
    color: red;
    font-size: 0.875em;
  }
  
  .confirmation {
    margin-top: 15px;
    padding: 10px;
    background-color: #e0ffe0;
    border: 1px solid #b2ffb2;
    border-radius: 4px;
  }
  
  button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: #4e0fed;
    color: white;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0fe31a;
  }
  </style>
  