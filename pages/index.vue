<script setup lang="ts">
const { data } = await useFetch('https://drvcash.com/api/collections')
</script>

<template>
  <div>
    <div class="container">
      <h3 class="mb-4">Diteolog Assistant</h3>
      <div class="row">
        <div class="col-md-4">
          <article>
            <h4>Common statistic</h4>
            <p>Collections length - {{ data.collections.length }}</p>
          </article>
        </div>
        <div class="col-md-4">
          <article>
            <h4>Collections name</h4>
            <ul>
              <li v-for="collection in data.collections" :key="collection.name">
                <!-- <NuxtLink t>{{ collection.name }}123</NuxtLink> -->
                <a :href="'/collections/' + collection.name">{{ collection.name }}</a>
              </li>
            </ul>
          </article>
        </div>
        <div class="col-md-4">

        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
  ul {
    li {
      a {
        color: #000
      }
    }
  }
</style>