<script setup>
import {ref, onMounted} from 'vue'
import axios from 'axios'
import moment from 'moment'
const baseUrl = ref('https://www.bseindia.com/xml-data/corpfiling/AttachLive/')

const notices = ref()
onMounted(async() =>{
  let notice = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w?pageno=1&strCat=-1&strPrevDate=&strScrip=&strSearch=P&strToDate=&strType=C')
  notices.value = notice.data.Table
  let ofs = await axios.get('https://www1.nseindia.com/live_market/content/live_watch/offer_sale/ofs_details_retail.json')
  console.log(ofs)
})
</script>

<template>
  <div class="bg-gray-50">
    <div class="mx-auto max-w-screen-xl px-4 py-12 sm:px-6 lg:flex lg:items-center lg:justify-between lg:py-16 lg:px-8">
    <ul v-if="notices">
      <li v-for="notice in notices" :key="notice.NEWSID" class="py-8">
        <a target="_blank" :href = "baseUrl+notice.ATTACHMENTNAME"> {{ notice.NEWSSUB}} </a><br />
        <span>{{ moment(notice.NEWS_DT).format('DD-MM-YYYY @ hh:mm')}}</span>
      </li>
    </ul>
    </div>
    <pre>{{notices}}</pre>
  </div>
</template>
