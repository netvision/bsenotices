<template>
  <div>
    <header class="bg-white shadow" v-if="$route.meta.title">
      <div class="mx-auto max-w-7xl px-4 py-6 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold leading-tight text-gray-900">
          {{ $route.meta.title }} <span class="text-base pl-6 font-mono">{{moment().format('dddd, MMMM Do YYYY')}}</span>
        </h1>
      </div>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>
<script setup>
import moment from 'moment'
</script>
