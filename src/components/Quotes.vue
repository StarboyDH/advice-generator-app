<script>
export default {
  name: "Quotes",
  data() {
    return {
      data: null,
      id: null,
      advice: null,
      imgSrc: null,
    };
  },

  methods: {
    async fetchAdvice() {
      try {
        const res = await fetch("https://api.adviceslip.com/advice");

        console.log(res.ok, res.status);
        this.data = await res.json();
        this.id = this.data.slip.id;
        this.advice = this.data.slip.advice;
      } catch (err) {
        console.log(err);
        this.id = "000";
        this.advice = "SOME ERROR OCCURRED.";
      }
    },

    rotateDice() {
      this.$refs.dice.style.animation = "rotatedice .5s ease forwards";
    },
  },

  mounted() {
    const screenWidth = window.screen.width;
    if (screenWidth < 1024) {
      this.imgSrc = "images/pattern-divider-mobile.svg";
    } else {
      this.imgSrc = "images/pattern-divider-desktop.svg";
    }

    this.fetchAdvice();
  },
};
</script>

<template>
  <div class="advice-container" @click="rotateDice()">
    <strong class="advice-number"
      >Advice #<span>{{ id }}</span></strong
    >
    <p class="advice">"{{ advice }}"</p>
    <img class="divider" :src="imgSrc" />
    <button class="btn" @click="fetchAdvice()">
      <img ref="dice" class="dice" src="images/icon-dice.svg" />
    </button>
  </div>
</template>

<style>
.advice-container {
  margin: 1rem;
  padding: 3rem 1rem 1rem 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Varela Round', sans-serif;
  text-align: center;
  background-color: #313a49;
  border-radius: 0.5rem;
}

.advice-number {
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 3px;
  color: hsl(151, 100%, 66%);
}

.advice {
  padding: 2rem 1rem 1rem 1rem;
  font-size: 22px;
  font-weight: 700;
  line-height: 1.6;
}

.divider {
  transform: translateY(100%);
}

.btn {
  width: 4rem;
  aspect-ratio: 1;
  transform: translateY(80%);
  display: grid;
  place-items: center;
  border: 1px solid hsl(151, 100%, 66%);
  border-radius: 50%;
  background-color: hsl(151, 100%, 66%);
  transition: 0.2s ease;
  cursor: pointer;
}

.btn:hover {
  box-shadow: 0 0 2rem 0 hsl(151, 100%, 66%);
}

@keyframes rotatedice {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

@media screen and (min-width: 1024px) {
  .advice-container {
    width: 40vw;
  }
}
</style>
