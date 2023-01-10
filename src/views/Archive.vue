<template>
  <div class="bg-gray-50">
    <div class="bg-gray-100 py-3 flex flex-col sm:py-12">
      
          <div class="max-w-md mx-auto">
            <div class="flex items-center space-x-5">
              <div class="block font-semibold text-2xl self-start text-gray-700">
                <h2 class="leading-relaxed">Search Archive</h2>
              </div>
            </div>
            <div class="divide-y divide-gray-200">
              <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                
                <div class="flex items-center space-x-4">
                  <div class="flex flex-col">
                    <label class="leading-loose">From</label>
                    <div class="relative focus-within:text-gray-600 text-gray-400">
                      <input v-model="data.strPrevDate" type="date" class="form-date form-input pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600" placeholder="25/02/2020">
                      <div class="absolute left-3 top-2">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path></svg>
                      </div>
                    </div>
                  </div>
                  <div class="flex flex-col">
                    <label class="leading-loose">To</label>
                    <div class="relative focus-within:text-gray-600 text-gray-400">
                      <input v-model="data.strToDate" type="date" class="form-date form-input pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600" placeholder="26/02/2020">
                      <div class="absolute left-3 top-2">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path></svg>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="flex items-center space-x-4">
                  <div class="flex flex-col w-40">
                      <label class="leading-loose">Scrip Code</label>
                      <div class="relative focus-within:text-gray-600 text-gray-400">
                        <input v-model="data.strScrip" type="number" class="form-number form-input pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">
                      </div>
                  </div>
                  <div class="flex flex-col">
                    <label class="leading-loose">Category</label>
                    <select v-model="data.strCat" class="form-select px-4 py-3 rounded-full">
                      <option value="-1" selected="selected">--Select Category--</option>
                      <option value="AGM/EGM">AGM/EGM</option>
                      <option value="Board Meeting">Board Meeting</option>
                      <option value="Company Update">Company Update</option>
                      <option value="Corp. Action">Corp. Action</option>
                      <option value="Insider Trading / SAST">Insider Trading / SAST</option>
                      <option value="Result">Result</option><option value="New Listing">New Listing</option>
                    </select>
                  </div>
              </div>
              </div>
              <div class="pt-4 flex items-center space-x-4">
                  <button class="bg-blue-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none" @click="getData">Search</button>
              </div>
            </div>
          </div>
          <div class="flex flex-col gap-4 items-center justify-center mt-4">
            <VueTailwindPagination v-if="total > 50"
              :current="data.pageno"
              :total="total"
              :per-page="50"
              @page-changed="onPageClick($event)"
            />
            <div v-for="d in announcements" :key="d.NEWSID" class="rounded-sm w-9/12 grid grid-cols-12 bg-white shadow p-3 gap-2 items-center hover:shadow-lg transition delay-150 duration-300 ease-in-out hover:scale-105 transform" href="#">
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
            <VueTailwindPagination v-if="total > 50"
              :current="data.pageno"
              :total="total"
              :per-page="50"
              @page-changed="onPageClick($event)"
            />
          </div>
          
        </div>
      
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import moment from 'moment'
import '@ocrv/vue-tailwind-pagination/styles'
import VueTailwindPagination from "@ocrv/vue-tailwind-pagination"
const total = ref(1)
const data = ref({
  pageno: 1,
  strCat: -1,
  strPrevDate:'',
  strToDate:'',
  strScrip:'',
  strSearch:'P',
  strType:'C'
})

const announcements = ref([])
const baseUrl = 'https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w'

const getData = async() => {
  let res = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w', {params: data.value})
  console.log(res.data)
  announcements.value = res.data.Table
  total.value = res.data.Table1[0].ROWCNT
}

const onPageClick = (p) => {
  data.value.pageno = p
  getData()
}

onMounted(async() => {
  let res = await axios.get('https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w', {params: data.value})
  console.log(res.data)
})
// https://api.bseindia.com/BseIndiaAPI/api/AnnGetData/w?pageno=1&strCat=-1&strPrevDate=&strScrip=&strSearch=P&strToDate=&strType=C
</script>
