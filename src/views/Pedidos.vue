<template>
  <div class="main-container">
    <h1>PEDIDOS</h1>
    <br />

    <div>
      <button 
        @click="selectCurrentIngredientType(ingredientType)" 
        v-for="ingredientType in availableIngredientTypes" 
        :key="ingredientType">
          {{ingredientType}}
      </button>
    </div>

    <ul>
      <li 
        v-for="ingredient in specificIngredientsList" 
        :key="ingredient.id">
          {{ingredient.tipo}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ingredientsList: null,
      specificIngredientsList: null,
      currentIngredientsType: null,
      availableIngredientTypes: ["paes", "carnes", "opcionais"]
    }
  },
  
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.ingredientsList = data;
    },
    selectCurrentIngredientType(ingredientType){
      this.currentIngredientsType = ingredientType;
      this.specificIngredientsList = this.ingredientsList[ingredientType];
    }
  },

  mounted() {
    this.getIngredientes();
  }
}
</script>
