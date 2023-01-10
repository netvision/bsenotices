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
    <div class="bg-gray-200 flex flex-col gap-4 items-center justify-center">
      <div v-for="d in newNotices" :key="d.NEWSID" class="rounded-sm w-1/2 grid grid-cols-12 bg-white shadow p-3 gap-2 items-center hover:shadow-lg transition delay-150 duration-300 ease-in-out hover:scale-105 transform" href="#">
              <div class="col-span-12 md:col-span-1">
                <a :href="'https://www.bseindia.com/xml-data/corpfiling/AttachLive/'+d.ATTACHMENTNAME" target="_blank">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 bi bi-file-pdf" fill="currentColor" viewBox="0 0 16 16">
                    <path d="M4 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H4zm0 1h8a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1z"/>
                    <path d="M4.603 12.087a.81.81 0 0 1-.438-.42c-.195-.388-.13-.776.08-1.102.198-.307.526-.568.897-.787a7.68 7.68 0 0 1 1.482-.645 19.701 19.701 0 0 0 1.062-2.227 7.269 7.269 0 0 1-.43-1.295c-.086-.4-.119-.796-.046-1.136.075-.354.274-.672.65-.823.192-.077.4-.12.602-.077a.7.7 0 0 1 .477.365c.088.164.12.356.127.538.007.187-.012.395-.047.614-.084.51-.27 1.134-.52 1.794a10.954 10.954 0 0 0 .98 1.686 5.753 5.753 0 0 1 1.334.05c.364.065.734.195.96.465.12.144.193.32.2.518.007.192-.047.382-.138.563a1.04 1.04 0 0 1-.354.416.856.856 0 0 1-.51.138c-.331-.014-.654-.196-.933-.417a5.716 5.716 0 0 1-.911-.95 11.642 11.642 0 0 0-1.997.406 11.311 11.311 0 0 1-1.021 1.51c-.29.35-.608.655-.926.787a.793.793 0 0 1-.58.029zm1.379-1.901c-.166.076-.32.156-.459.238-.328.194-.541.383-.647.547-.094.145-.096.25-.04.361.01.022.02.036.026.044a.27.27 0 0 0 .035-.012c.137-.056.355-.235.635-.572a8.18 8.18 0 0 0 .45-.606zm1.64-1.33a12.647 12.647 0 0 1 1.01-.193 11.666 11.666 0 0 1-.51-.858 20.741 20.741 0 0 1-.5 1.05zm2.446.45c.15.162.296.3.435.41.24.19.407.253.498.256a.107.107 0 0 0 .07-.015.307.307 0 0 0 .094-.125.436.436 0 0 0 .059-.2.095.095 0 0 0-.026-.063c-.052-.062-.2-.152-.518-.209a3.881 3.881 0 0 0-.612-.053zM8.078 5.8a6.7 6.7 0 0 0 .2-.828c.031-.188.043-.343.038-.465a.613.613 0 0 0-.032-.198.517.517 0 0 0-.145.04c-.087.035-.158.106-.196.283-.04.192-.03.469.046.822.024.111.054.227.09.346z"/>
                  </svg>
                </a>
              </div>
              <div class="col-span-11 xl:-ml-5">
                <p class="font-light font-mono text-sm">{{ moment(d.NEWS_DT).format('MMMM Do YYYY, h:mm:ss a') }}</p>
                <p class="text-blue-600 font-semibold"><a :href="d.NSURL" target="_blank"> {{ d.NEWSSUB }}</a></p>
                <p class="text-sm font-serif text-lime-800 italic">{{d.CATEGORYNAME}}</p>
              </div>
              <!-- Description -->
              <div class="md:col-start-2 col-span-11 xl:-ml-5">
                <p class="text-sm text-gray-800 font-light"> {{ d.HEADLINE }}</p>
                <p class="text-sm text-gray-600 font-light"> {{ d.MORE }} </p>
              </div>
      </div>
    </div>
    </div>
    <div class="mx-auto max-w-screen-xl px-4 py-12 sm:px-6 lg:py-16 lg:px-8">
      <div v-for="d in notices" :key="d.NEWSID" class="rounded-sm w-full grid grid-cols-12 bg-white shadow p-3 m-2 gap-4 items-center hover:shadow-lg transition delay-150 duration-300 ease-in-out hover:scale-105 transform" href="#">
              <div class="col-span-12 md:col-span-1">
                <a :href="'https://www.bseindia.com/xml-data/corpfiling/AttachLive/'+d.ATTACHMENTNAME" target="_blank">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 bi bi-file-pdf" fill="currentColor" viewBox="0 0 16 16">
                    <path d="M4 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H4zm0 1h8a1 1 0 0 1 1 1v12a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1z"/>
                    <path d="M4.603 12.087a.81.81 0 0 1-.438-.42c-.195-.388-.13-.776.08-1.102.198-.307.526-.568.897-.787a7.68 7.68 0 0 1 1.482-.645 19.701 19.701 0 0 0 1.062-2.227 7.269 7.269 0 0 1-.43-1.295c-.086-.4-.119-.796-.046-1.136.075-.354.274-.672.65-.823.192-.077.4-.12.602-.077a.7.7 0 0 1 .477.365c.088.164.12.356.127.538.007.187-.012.395-.047.614-.084.51-.27 1.134-.52 1.794a10.954 10.954 0 0 0 .98 1.686 5.753 5.753 0 0 1 1.334.05c.364.065.734.195.96.465.12.144.193.32.2.518.007.192-.047.382-.138.563a1.04 1.04 0 0 1-.354.416.856.856 0 0 1-.51.138c-.331-.014-.654-.196-.933-.417a5.716 5.716 0 0 1-.911-.95 11.642 11.642 0 0 0-1.997.406 11.311 11.311 0 0 1-1.021 1.51c-.29.35-.608.655-.926.787a.793.793 0 0 1-.58.029zm1.379-1.901c-.166.076-.32.156-.459.238-.328.194-.541.383-.647.547-.094.145-.096.25-.04.361.01.022.02.036.026.044a.27.27 0 0 0 .035-.012c.137-.056.355-.235.635-.572a8.18 8.18 0 0 0 .45-.606zm1.64-1.33a12.647 12.647 0 0 1 1.01-.193 11.666 11.666 0 0 1-.51-.858 20.741 20.741 0 0 1-.5 1.05zm2.446.45c.15.162.296.3.435.41.24.19.407.253.498.256a.107.107 0 0 0 .07-.015.307.307 0 0 0 .094-.125.436.436 0 0 0 .059-.2.095.095 0 0 0-.026-.063c-.052-.062-.2-.152-.518-.209a3.881 3.881 0 0 0-.612-.053zM8.078 5.8a6.7 6.7 0 0 0 .2-.828c.031-.188.043-.343.038-.465a.613.613 0 0 0-.032-.198.517.517 0 0 0-.145.04c-.087.035-.158.106-.196.283-.04.192-.03.469.046.822.024.111.054.227.09.346z"/>
                  </svg>
                </a>
              </div>
              <div class="col-span-11 xl:-ml-5">
                <p class="font-light font-mono text-sm">{{ moment(d.NEWS_DT).format('MMMM Do YYYY, h:mm:ss a') }}</p>
                <p class="text-blue-600 font-semibold"><a :href="d.NSURL" target="_blank"> {{ d.NEWSSUB }}</a></p>
                <p class="text-sm font-serif text-lime-800 italic">{{d.CATEGORYNAME}}</p>
              </div>
              <!-- Description -->
              <div class="md:col-start-2 col-span-11 xl:-ml-5">
                <p class="text-sm text-gray-800 font-light"> {{ d.HEADLINE }}</p>
                <p class="text-sm text-gray-600 font-light"> {{ d.MORE }} </p>
              </div>
            </div>
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
  console.log()
}

onMounted(async() =>{
  let notice = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w?pageno=1&strCat=-1&strPrevDate=&strScrip=&strSearch=P&strToDate=&strType=C')
  notices.value = notice.data.Table
  setInterval(getNotices, 10000)
})
</script>
