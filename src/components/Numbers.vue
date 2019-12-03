<template>
  <div>
    <div
      class="number"
      :id="'number-'+number"
      v-for="number in n()"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset"
    >{{number}}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      limit: this.$parent.limit,
      numbers: []
    };
  },
  watch: {
    ["$parent.limit"](newLimit) {
      while (newLimit > 0) {
        // This limits the limiter so the value cannot be negeative.
        while (newLimit <= 100) {
          // This limits the limiter so the value cannot be higher than 100.
          this.limit = newLimit;
        }
        newLimit = 100;
        this.limit = newLimit; //if the input value exceed 100 then it will return 100
      }
      newLimit = 1;
      this.limit = newLimit; //if the input value is negative it will return 1.
    }
  },
  methods: {
    n() {
      let numbers = [];     // initialisng the array for numbers
      for (var i = 0; i < this.limit; i++) { //a loop based on the input called this.limit value set as the maximum size
        numbers = [...numbers, i + 1]; // initialising the values into an array basuse on array index. Added the +1 to i as it goes by array index to show 1-100 instead of 0 - 99
      }
      return numbers.sort(() => Math.random() - 0.5); //randomises the array values
    },
    hov(number) {
      const nums = document.querySelectorAll(".number"); // This returns all values within the set parameter number
      for (let i = 0; i < nums.length; i++) { 
        const num = nums[i].textContent.trim();
        if (number % num === 0 && number != num) { // uses the highlighted number and finds all of it's divisible numbers, added the "number != num" to remove the hovered number from being highlighted
            nums[i].classList.add("active"); // whem the number is divisable and has no remainder, it'll assign that number as active
            // console.log("divisor", num); in the console it will print all the numbers that are divisor of the hovered number
          }
      }
    },
    reset() { 
      const nums = document.querySelectorAll(".number"); // This returns all values
      nums.forEach(num => num.classList.remove("active")); // looping to see if any numbers are assigned active and then removing them
    }
  }
};
</script>

<style scoped>
.number {
  display: inline-block;
  padding: 5px;
  background-color: lightgreen;
  margin: 5px;
}

.active {
  background-color: red;
}
</style>
