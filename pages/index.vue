<template>
  <div class="container">
    <div>
      <logo/>
      <h1 class="title">
        test
      </h1>
      <h2 class="subtitle">
        My riveting Nuxt.js project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
        <h2>useAsync</h2>
        <div v-if="isLoading">Loading...</div>
        <div v-else-if="error">Error!</div>
        <pre v-else>{{ data }}</pre>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
    import Logo from '~/components/Logo.vue'
    import {createComponent} from "@vue/composition-api";
    import {useAsync} from "vue-async-function/dist";

    async function wait({millis}: { millis: number }): Promise<string> {
        console.log("wait called");
        return new Promise(resolve => {
            setTimeout(() => resolve(`Done waiting ${millis} milliseconds!`), millis);
        });
    }

    export default createComponent({
        components: {
            Logo
        },
        setup(_props,_context) {
            console.log("Setup");
            const {data, error, isLoading} = useAsync(wait, {millis: 2000});
            return {data, error, isLoading};
        }
    })
</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .title {
    font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }
</style>
