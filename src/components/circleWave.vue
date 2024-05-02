<template>
  <div class="circle">
    <span class="circle__btn" :class="{ shadow: !isAnimate }">
      <slot />
    </span>
    <span class="circle__back-1" :class="{ paused: !isAnimate }"></span>
    <span class="circle__back-2" :class="{ paused: !isAnimate }"></span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'CircleWave',
  props: {
    isAnimate: {
      type: Boolean,
      default: false
    }
  }
})
</script>

<style lang="scss">
$shadow:
  0.3rem 0.3rem 0.6rem var(--greyLight-2),
  -0.2rem -0.2rem 0.5rem var(--white);
$inner-shadow:
  inset 0.2rem 0.2rem 0.5rem var(--greyLight-2),
  inset -0.2rem -0.2rem 0.5rem var(--white);

/*  PLAY BUTTON  */
.circle {
  grid-column: 2 / 3;
  grid-row: 4 / 6;
  justify-self: center;
  border-radius: 1rem;
  display: grid;
  grid-template-rows: 1fr;
  justify-items: center;
  align-items: center;

  &__btn {
    grid-row: 1 / 2;
    grid-column: 1 / 2;
    padding: 6px;
    display: flex;
    margin: 0.6rem;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    font-size: 3.2rem;
    color: var(--primary);
    z-index: 300;
    background: var(--greyLight-1);
    box-shadow: $shadow;
    cursor: pointer;
    position: relative;
    &.shadow {
      box-shadow: $inner-shadow;
    }

    .play {
      position: absolute;
      opacity: 0;
      transition: all 0.2s linear;
      &.visibility {
        opacity: 1;
      }
    }
    .pause {
      position: absolute;
      transition: all 0.2s linear;
      &.visibility {
        opacity: 0;
      }
    }
  }

  &__back-1,
  &__back-2 {
    grid-row: 1 / 2;
    grid-column: 1 / 2;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    filter: blur(1px);
    z-index: 100;
  }

  &__back-1 {
    box-shadow:
      0.4rem 0.4rem 0.8rem var(--greyLight-2),
      -0.4rem -0.4rem 0.8rem var(--white);
    background: linear-gradient(to bottom right, var(--greyLight-2) 0%, var(--white) 100%);
    animation: waves 4s linear infinite;

    &.paused {
      animation-play-state: paused;
    }
  }

  &__back-2 {
    box-shadow:
      0.4rem 0.4rem 0.8rem var(--greyLight-2),
      -0.4rem -0.4rem 0.8rem var(--white);
    animation: waves 4s linear 2s infinite;

    &.paused {
      animation-play-state: paused;
    }
  }
}

@keyframes waves {
  0% {
    transform: scale(1);
    opacity: 1;
  }

  50% {
    opacity: 1;
  }

  100% {
    transform: scale(2);
    opacity: 0;
  }
}
</style>