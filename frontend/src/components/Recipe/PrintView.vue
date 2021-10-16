<template>
  <div class="container print">
    <div id="cust-header">
      <div id="cust-picture" v-bind:style="{backgroundImage: 'url('+getImage(recipe.slug)+')'}">

      </div>
      <div id="cust-title">
        <h1>
          {{ recipe.name }}
        </h1>
        <!--
        <vue-markdown :source="recipe.description"> </vue-markdown>
        -->
      </div>
      <div id="cust-headfooter">
        <div class="yield">
          <span v-if="recipe.recipeYield">
            <v-icon
              small
            >
              {{ $globals.icons.yield }}
            </v-icon>
            {{ recipe.recipeYield }}
          </span>
        </div>
        <div class="time">
          <span v-if="recipe.totalTime" style="margin-right:10px">
            <v-icon
              small
            >
              {{ $globals.icons.stove }}
            </v-icon>
            {{ recipe.totalTime }}
          </span>
        </div>
      </div>
    </div>
    <!--
    <div class="time-container">
    <RecipeTimeCard :prepTime="recipe.prepTime" :totalTime="recipe.totalTime" :performTime="recipe.performTime" />
    </div>
    -->


    <!--
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
    -->
    <div id="cust-leftcol">
      <div id="cust-ingredients">
        <h2>{{ $t("recipe.ingredients") }}</h2>
        <ul>
          <template v-for="(ingredient, index) in recipe.recipeIngredient">
            <template v-if="ingredient.title">
              <li :key="index" class="cust-title"><p>{{ ingredient.title }}:</p></li>
            </template>
            <li :key="index"><p>{{ ingredient.note }}</p></li>

          </template>
        <!--
          <li v-for="(ingredient, index) in recipe.recipeIngredient" :key="index">
            <p>{{ ingredient.note }}</p>
          </li>
        -->
        </ul>
      </div>
      <div id="cust-nutritions">
        <div>
        <span v-if="recipe.nutrition.calories" class="nutrition">
          {{ recipe.nutrition.calories }} kcal
        </span>
        </div>
        <span v-if="recipe.nutrition.fatContent" class="nutrition">
          F: {{ recipe.nutrition.fatContent }} g
        </span>
        <span v-if="recipe.nutrition.carbohydrateContent" class="nutrition">
          KH: {{ recipe.nutrition.carbohydrateContent }} g
        </span>
        <span v-if="recipe.nutrition.proteinContent" class="nutrition">
          E: {{ recipe.nutrition.proteinContent }} g
        </span>
      </div>
    </div>
    <div id="cust-instructions">
      <h2>{{ $t("recipe.instructions") }}</h2>
      <div v-for="(step, index) in recipe.recipeInstructions" :key="index">
        <h2 v-if="step.title">{{ step.title }}</h2>
        <div class="ml-5">
          <!-- <h3>{{ $t("recipe.step-index", { step: index + 1 }) }}</h3> -->
          <!-- <h3>{{ $t("recipe.step-index", { step: index + 1 }) }}</h3> -->
          <vue-markdown :source="index+1+'\\. '+step.text"> </vue-markdown>
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
//import RecipeTimeCard from "@/components/Recipe/RecipeTimeCard.vue";
import VueMarkdown from "@adapttive/vue-markdown";
import { api } from "@/api";
export default {
  components: {
    //RecipeTimeCard,
    VueMarkdown,
  },
  props: {
    recipe: Object,
  },
  methods: {
    getImage(slug) {
      if (slug) {
        return api.recipes.recipeImage(slug, 1, this.recipe.image);
      }
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat');
@media print {
  body,
  html {
    margin-top: -40px !important;
  }
  .theme--dark.v-application {
    background-color: transparent;
    color: #000;
  }
}

h1 {
  margin: 0 auto;
  font-size: 28px;
  letter-spacing: -0.015625em;
  font-weight: 300;
  padding: 0;
  text-align: center;
  height:115px;
}

h2 {
  font-size: 16px;
  margin-bottom: 0.25rem;
  margin-top: 10px;
  margin-left: 5px;
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

.nutrition {
  margin-right:5px;
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


#cust-header {
  background-color: #f5f5f5;
  width: 100%;
  height: 150px;
}
#cust-headfooter {
  margin-left: 30px;
  padding-left: 30px;
  font-size: 10px;
}
#cust-headfooter .yield {
}
#cust-headfooter .time {
}
#cust-picture {
  float: left;
  margin-right: 20px;
  height: 150px;
  width: 175px;
  background-size: cover;
  background-position: center center;
}
#cust-leftcol {
  background-color: #f0f7f4;
  margin-right:20px;
  float: left;
  height: 640px;
  width: 175px;
}
#cust-ingredients {
  margin-left: 10px;
  height: 593px;
}
#cust-ingredients .cust-title {
  font-weight: bold;
  text-decoration:underline;
  margin-top:10px;
}

#cust-nutritions {
  padding: 0 12px 0 12px;
  font-size: 10px;
}
#cust-instructions {
  margin-top: -25px;
}
#cust-instructions h2 {
  margin-bottom: 20px;
}

@page {
  size: A4;
  margin: 42.6mm 31mm;
}
@media print {
  .print {
    display: initial;
    /* position: fixed;
    top:0; */
    font-family:'Montserrat';
  }
  .container {
    padding: 1px;
    background-color:#fefefe;
    /* margin:43.5mm 31mm; */
  }
  .v-application ul {
    padding-left: 0;
  }
  p {
    font-size: 10px;
  }
  li {
    margin-bottom: 4px;
  }
}
</style>
