<template>
  <Person :data="currentPerson" />
  <Options
    @submitted-to-parent="this.receiveAnswer"
    :optionData="this.options"
    :numOfOptions="this.numOfOptions"
    :currentPerson="this.currentPerson"
  />
</template>

<script>
import Person from "./components/Person.vue";
import Options from "./components/Options.vue";
import staffImport from "./staff.json";
export default {
  name: "App",
  components: {
    Person,
    Options,
  },
  data() {
    return {
      staff: staffImport,
      finished: false,
      currentPerson: null,
      score: 0,
      numOfOptions: 3,
    };
  },
  methods: {
    setCurrentPerson() {
      let numOfUnanswered = this.staff.filter(
        (person) => person.state === "unanswered"
      );
      let random = Math.floor(Math.random() * numOfUnanswered.length);
      this.currentPerson = this.staff[random];
    },
    receiveAnswer() {
      this.setCurrentPerson();
      this.setOptions();
    },
    setOptions() {
      let optionsContainer = [];
      optionsContainer.push(this.currentPerson);
      //loop through all staff
      for (let i = 0; i <= this.staff.length; i++) {
        //check if the option amount is enough
        if (optionsContainer.length < this.numOfOptions) {
          //randomize a pick among staff
          let random = Math.floor(Math.random() * this.staff.length);
          //check that the randomized person is NOT current person
          if (this.staff[random].id !== this.currentPerson.id) {
            //check if optionsContainer is populated
            if (
              optionsContainer.length > 0 &&
              this.staff[random].gender === this.currentPerson.gender
            ) {
              //and in that case loop through options to check that we don't push duplicates
              let alreadyThere = optionsContainer.find(
                (person) => person.id === this.staff[random].id
              );
              if (!alreadyThere) {
                optionsContainer.push(this.staff[random]);
              }
            } else if (
              this.staff[random].gender === this.currentPerson.gender
            ) {
              optionsContainer.push(this.staff[random]);
            }
          }
        }
      }
      this.options = optionsContainer;
      console.log(this.options);
    },
    setCurrentToCompleted() {
      let currentId = this.staff.findIndex(
        (person) => person.id === this.currentPerson.id
      );
      this.staff[currentId].state = "answered";
    },

    checkAnswer() {
      // if answer is right, randomize a new person and make this persons state "correct"
      //if answer is wrong,
      // randomize a new person and make this persons state "incorrect" and remove one life
    },
  },
  beforeMount() {
    this.setCurrentPerson();
    this.setOptions();
  },
  watch: {
    currentPerson() {
      this.setOptions();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.options {
  display: flex;
  justify-content: center;
}
</style>
