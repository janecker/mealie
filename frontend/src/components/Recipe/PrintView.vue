<template>
  <div class="container print">
    <div>
      <h1>
        {{ recipe.name }}
      </h1>
    </div>
    <div class="time-container">
      <RecipeTimeCard :prepTime="recipe.prepTime" :totalTime="recipe.totalTime" :performTime="recipe.performTime" />
    </div>
    <v-btn
      v-if="recipe.recipeYield"
      dense
      small
      :hover="false"
      type="label"
      :ripple="false"
      elevation="0"
      color="secondary darken-1"
      class="rounded-sm static"
    >
      {{ recipe.recipeYield }}
    </v-btn>
    <div id="cust-ingredients">
      <vue-markdown :source="recipe.description"> </vue-markdown>
      <h2>{{ $t("recipe.ingredients") }}</h2>
      <ul>
        <li v-for="(ingredient, index) in recipe.recipeIngredient" :key="index">
          <p>{{ ingredient.note }}</p>
        </li>
      </ul>
    </div>
    <div>
      <h2>{{ $t("recipe.instructions") }}</h2>
      <div v-for="(step, index) in recipe.recipeInstructions" :key="index">
        <h2 v-if="step.title">{{ step.title }}</h2>
        <div class="ml-5">
          <h3>{{ $t("recipe.step-index", { step: index + 1 }) }}</h3>
          <vue-markdown :source="step.text"> </vue-markdown>
        </div>
      </div>

      <br />
      <v-divider v-if="recipe.notes.length > 0" class="mb-5 mt-0"></v-divider>

      <div v-for="(note, index) in recipe.notes" :key="index + 'note'">
        <h3>{{ note.title }}</h3>
        <vue-markdown :source="note.text"> </vue-markdown>
      </div>
    </div>
  </div>
</template>

<script>
import RecipeTimeCard from "@/components/Recipe/RecipeTimeCard.vue";
import VueMarkdown from "@adapttive/vue-markdown";
export default {
  components: {
    RecipeTimeCard,
    VueMarkdown,
  },
  props: {
    recipe: Object,
  },
};
</script>

<style>
@media print {
  body,
  html {
    margin-top: -40px !important;
  }
}

h1 {
  margin-top: 0 !important;
  display: -webkit-box;
  display: flex;
  font-size: 2rem;
  letter-spacing: -0.015625em;
  font-weight: 300;
  padding: 0;
}

h2 {
  margin-bottom: 0.25rem;
}

h3 {
  margin-bottom: 0.25rem;
}

ul {
  padding-left: 1rem;
}

li {
  display: -webkit-box;
  display: -webkit-flex;
  margin-left: 0;
  margin-bottom: 0.5rem;
}

li p {
  margin-left: 0.25rem;
  margin-bottom: 0 !important;
}

p {
  margin: 0;
  font-size: 1rem;
  letter-spacing: 0.03125em;
  font-weight: 400;
}

.icon {
  margin-top: auto;
  margin-bottom: auto;
  margin-right: 0.5rem;
  height: 3rem;
  width: 3rem;
}

.time-container {
  display: flex;
  justify-content: left;
}

.time-chip {
  border-radius: 0.25rem;
  border-color: black;
  border: 1px;
  border-top: 1px;
}

.print {
  display: none;
}

#cust-ingredients {
  float: left;
}

@media print {
  .print {
    display: initial;
  }
}
</style>
