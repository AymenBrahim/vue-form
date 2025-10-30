<script setup lang="ts">
import { ref } from 'vue'
import FormField from './form/FormField.vue'
import ButtonComponent from './ButtonComponent.vue'

const isExpanded = ref(false)

const toggle = () => (isExpanded.value = !isExpanded.value)

const options = [
  { label: 'less than $50K', value: '<50K' },
  { label: '$50K-$150K', value: '$50K-$150K' },
  { label: '$150K-$300K', value: '$150K-$300K' },
  { label: '$300K-$500K', value: '$300K-$500K' },
]
</script>
<template>
  <ButtonComponent style="margin-left: auto" small @click="toggle" aria-label="contact"
    >contact</ButtonComponent
  >
  <div :class="['drawer', isExpanded && 'is-expanded']">
    <ButtonComponent class="close" small @click="toggle" aria-label="close">close</ButtonComponent>
    <form>
      <div class="form-container">
        <FormField
          class="half"
          name="first_name"
          label="first name"
          type="text"
          :error="'a custom error'"
          required
        />
        <FormField class="half" name="last_name" label="last name" type="text" required />
        <FormField class="half" name="company_name" label="company name" type="text" required />
        <FormField class="half" name="email" label="your email" type="email" required />
        <FormField
          name="project_type"
          label="project type"
          type="multiCheck"
          :options="[
            { label: 'brand', value: 'brand' },
            { label: 'website', value: 'website' },
            { label: 'art direction', value: 'art_direction' },
            { label: 'campaign', value: 'campaign' },
            { label: 'other', value: 'other' },
          ]"
          required
        />
        <FormField
          name="project_type"
          label="project type"
          type="textarea"
          placeholder="Type here..."
          required
        />

        <FormField
          class="half"
          name="budget_expectation"
          label="budget expectation"
          type="select"
          :options="options"
          required
        />
        <FormField
          class="half"
          name="timeline_expectation"
          label="timeline expectation"
          type="text"
          required
        />
        <!-- <FormField
            class="half"
            name="how_did_you_find_us"
            label="how did you find us"
            type="text"
            required
          />
          <FormField
            class="half"
            name="favorite_movie_or_album"
            label="favorite movie or album"
            type="text"
            required
          /> -->
      </div>
      <ButtonComponent style="position: relative" type="submit" aria-label="submit"
        >submit</ButtonComponent
      >
    </form>
  </div>
  <div class="backdrop"></div>
</template>

<style scoped>
.drawer {
  position: fixed;
  right: -100vw;
  top: 0;
  transform: scaleX(0);
  min-height: 100vh;
  height: 100%;
  width: 50vw;
  min-width: min(100%, 400px);

  background: var(--bg-primary);

  padding: 103px 16px 0 30px;
  overflow: scroll;
  z-index: 9999;
  transition: all 0.5s ease-in;
  box-sizing: border-box;
}
.close {
  position: fixed;
  top: 24px;
  right: 24px;
  z-index: var(--z-pop-over);
}
.form-container {
  --column-gap: 24px;
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  column-gap: var(--column-gap);

  box-sizing: border-box;
}
.form-container > * {
  width: 100%;
}
.form-container > .half {
  width: calc(50% - var(--column-gap) / 2);
}

.full-width {
  width: 100%;
}

.drawer.is-expanded {
  right: 0px;
  transform: scaleX(1);

  transition: all 0.5s ease-out;
}
.backdrop::after {
  content: '';
  position: fixed;
  inset: 0;
  width: 100vw;
  height: 100vh;

  background: var(--bg-primary);

  opacity: 0;
  z-index: 2;
  backdrop-filter: blur(4px);

  pointer-events: none;
  transition: all 0.5s ease-in;
}
.drawer.is-expanded + .backdrop::after {
  opacity: 0.8;
  transition: all 0.5s ease-out;
}

@media (prefers-reduced-motion: reduce) {
  .slide-enter-active,
  .slide-leave-active,
  .slide-enter-from,
  .slide-leave-to {
    transition: none;
  }
}
</style>
