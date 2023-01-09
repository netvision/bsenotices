<template>
  <div class="bg-gray-50">
    
    <div class="mx-auto max-w-screen-xl px-4 py-12 sm:px-6 lg:flex lg:items-center lg:justify-between lg:py-16 lg:px-8">
    <div class="relative text-gray-600 focus-within:text-gray-400">
      <span class="absolute inset-y-0 left-0 flex items-center pl-2">
        <button type="submit" class="p-1 focus:outline-none focus:shadow-outline">
          <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" class="w-6 h-6"><path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
        </button>
      </span>
      <input type="text" v-model="filter" @blur="setFilters" name="q" class="py-2 text-sm text-gray-700 bg-gray-100 rounded-md pl-10 focus:outline-none focus:bg-white focus:text-gray-900" placeholder="Filter..." autocomplete="off">
    </div>
    <ul v-if="newNotices">
      <li v-for="notice in newNotices" :key="notice.NEWSID" class="py-8 bg-green-400">
        <a target="_blank" :href = "baseUrl+notice.ATTACHMENTNAME"> {{ notice.NEWSSUB}} </a><br />
        <span v-html="notice.HEADLINE" />
        <span>{{ moment(notice.NEWS_DT).format('DD-MM-YYYY @ hh:mm')}}</span>
      </li>
    </ul>
    </div>
    <div class="mx-auto max-w-screen-xl px-4 py-12 sm:px-6 lg:flex lg:items-center lg:justify-between lg:py-16 lg:px-8">
    <ul v-if="notices">
      <li v-for="notice in notices" :key="notice.NEWSID" class="py-8">
        <a target="_blank" :href = "baseUrl+notice.ATTACHMENTNAME"> {{ notice.NEWSSUB}} </a><br />
        <span v-html="notice.HEADLINE"></span><br />
        <span>{{ moment(notice.NEWS_DT).format('DD-MM-YYYY @ hh:mm')}}</span>
      </li>
    </ul>
    </div>
  </div>
</template>
<script setup>
import {ref, onMounted} from 'vue'
import axios from 'axios'
import moment from 'moment'
const baseUrl = ref('https://www.bseindia.com/xml-data/corpfiling/AttachLive/')
const filter = ref()
const notices = ref()
const newNotices = ref([])
const filters = ref([])

var audio = new Audio('/notification.wav')

const setFilters = () => {
  if(filter.value){
    let fils = filter.value.split(',')
    if(fils.length > 0){
      filters.value = fils.map(f => f.trim())
    }
  }
  else filters.value = []
}
const getNotices = async() => {
  let newn = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w?pageno=1&strCat=-1&strPrevDate=&strScrip=&strSearch=P&strToDate=&strType=C')
  let newFiltered = (filters.value.length > 0) ? newn.data.Table.filter(el => filters.value.some(it => it == el.SCRIP_CD)) :  newn.data.Table
  let result = newFiltered.filter(o2 => !notices.value.some(o3 => o2.NEWSID === o3.NEWSID))
  if(result.length > 0) {
    audio.play()
  }
  notices.value = newFiltered
  console.log(newn.data)
}

onMounted(async() =>{
  let notice = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w?pageno=1&strCat=-1&strPrevDate=&strScrip=&strSearch=P&strToDate=&strType=C')
  notices.value = notice.data.Table
  setInterval(getNotices, 10000)
})
</script>
