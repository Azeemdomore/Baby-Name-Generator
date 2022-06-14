<script setup lang="ts">
import { Gender, Popularity, Length, names } from "./data";

interface OptionState {
  gender: string;
  popularity: string;
  length: string;
}

const computedSelectedNames = () => {
  const filterNames = names
    .filter((name) => name.gender === option.gender)
    .filter((name) => name.popularity === option.popularity)
    .filter((name) => {
      if (option.length === Length.ALL) return true;
      else return name.length === option.length;
    });

  selectedNames.value = filterNames.map((name) => name.name);
};
const selectedNames = ref<string[]>([]);

const option = reactive<OptionState>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT,
});
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your option and click the "Find Names" button below</p>
    <div class="main-container">
      <div>
        <h4>1) Choose a gender</h4>
        <div class="btn-container">
          <button
            :class="option.gender === Gender.BOY && 'btn-active'"
            @click="option.gender = Gender.BOY"
            class="btn-option btn-right"
          >
            Boy
          </button>
          <button
            :class="option.gender === Gender.GIRL && 'btn-active'"
            @click="option.gender = Gender.GIRL"
            class="btn-option btn-left"
          >
            Girl
          </button>
        </div>
      </div>
      <div>
        <h4>2) Choose the name's popularity</h4>
        <div class="btn-container">
          <button
            :class="option.popularity === Popularity.TRENDY && 'btn-active'"
            @click="option.popularity = Popularity.TRENDY"
            class="btn-option btn-right"
          >
            Trendy
          </button>
          <button
            :class="option.popularity === Popularity.UNIQUE && 'btn-active'"
            @click="option.popularity = Popularity.UNIQUE"
            class="btn-option btn-left"
          >
            Unique
          </button>
        </div>
      </div>
      <div>
        <h4>3) Choose name's length</h4>
        <div class="btn-container">
          <button
            :class="option.length === Length.ALL && 'btn-active'"
            @click="option.length = Length.ALL"
            class="btn-option btn-right"
          >
            All
          </button>
          <button
            :class="option.length === Length.SHORT && 'btn-active'"
            @click="option.length = Length.SHORT"
            class="btn-option"
          >
            Short
          </button>
          <button
            :class="option.length === Length.LONG && 'btn-active'"
            @click="option.length = Length.LONG"
            class="btn-option btn-left"
          >
            Long
          </button>
        </div>
      </div>
      <button @click="computedSelectedNames" class="primary">Find Names</button>
    </div>

    {{ selectedNames }}
  </div>
</template>
<style scoped>
.container {
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}
.main-container {
  background-color: silver;
  border-radius: 30px;
  padding: 1rem;
  margin-top: 40px;
}
.btn-option {
  border: none;
  outline: 0.1rem solid blue;
  width: 15%;
  padding: 0.5rem;
}
.btn-right {
  border-radius: 30px 0 0 30px;
}
.btn-left {
  border-radius: 0 30px 30px 0;
}
.btn-active {
  background-color: blue;
  color: white;
}
.primary {
  width: 20%;
  padding: 0.75rem;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 30px;
  margin: 2rem;
  cursor: pointer;
}
</style>
