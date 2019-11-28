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
      let numbers = [];
      for (var i = 0; i < this.limit; i++) {
        numbers = [...numbers, i + 1]; //the random numbers had to be between 1-100, so added the +1 to i as it goes by array index
      }
      return numbers.sort(() => Math.random() - 0.5);
    },
    hov(number) {
      const nums = document.querySelectorAll(".number");

      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent.trim();
        if (number % num === 0 && number != num) { // added the number != num to remove the hovered number from being highlighted
            nums[i].classList.add("active");
            console.log("divisor", num);
          }
      }
    },
    reset() {
      const nums = document.querySelectorAll(".number");
      nums.forEach(num => num.classList.remove("active"));
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
