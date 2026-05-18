<template>
  <div class="home">
    <header>
      <p>NEWS</p>
      <!-- 클릭 시 검색창 토글 -->
      <p class="svg" @click="isSearchOpen = !isSearchOpen" style="cursor: pointer;">
        <!-- 돋보기 모양 SVG (검색창이 닫혀있을 때 표시) -->
        <svg v-if="!isSearchOpen" width="18" height="18" viewBox="0 0 23 23" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M21.2111 23L13.1611 14.95C12.5222 15.4611 11.7875 15.8657 10.9569 16.1639C10.1264 16.462 9.24259 16.6111 8.30556 16.6111C5.98426 16.6111 4.01989 15.807 2.41245 14.1987C0.805001 12.5904 0.000852528 10.626 6.76073e-07 8.30556C-0.000851176 5.98511 0.803297 4.02074 2.41245 2.41244C4.02159 0.804148 5.98596 0 8.30556 0C10.6251 0 12.5899 0.804148 14.1999 2.41244C15.8099 4.02074 16.6137 5.98511 16.6111 8.30556C16.6111 9.24259 16.462 10.1264 16.1639 10.9569C15.8657 11.7875 15.4611 12.5222 14.95 13.1611L23 21.2111L21.2111 23ZM8.30556 14.0556C9.90278 14.0556 11.2606 13.4967 12.3791 12.3791C13.4976 11.2615 14.0564 9.90363 14.0556 8.30556C14.0547 6.70748 13.4959 5.35006 12.3791 4.23328C11.2623 3.1165 9.90448 2.55726 8.30556 2.55556C6.70663 2.55385 5.3492 3.11309 4.23328 4.23328C3.11735 5.35346 2.55811 6.71089 2.55556 8.30556C2.553 9.90022 3.11224 11.2581 4.23328 12.3791C5.35432 13.5001 6.71174 14.059 8.30556 14.0556Z" fill="white"/>
        </svg>
        <!-- X 모양 SVG (검색창이 열려있을 때 표시) -->
        <svg v-else width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M18 6L6 18M6 6L18 18" stroke="white" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </p>
      
      <!-- 검색창 영역 -->
      <div class="search" v-show="isSearchOpen">
        <!-- @submit.prevent는 input 엔터나 button 클릭 시 자동으로 실행됩니다 -->
        <form @submit.prevent="handleSearch">
          <input type="text" v-model="keyword" class="search_inp" />
          <button type="submit" class="search_btn">
            <svg width="14" height="14" viewBox="0 0 23 23" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M21.2111 23L13.1611 14.95C12.5222 15.4611 11.7875 15.8657 10.9569 16.1639C10.1264 16.462 9.24259 16.6111 8.30556 16.6111C5.98426 16.6111 4.01989 15.807 2.41245 14.1987C0.805001 12.5904 0.000852528 10.626 6.76073e-07 8.30556C-0.000851176 5.98511 0.803297 4.02074 2.41245 2.41244C4.02159 0.804148 5.98596 0 8.30556 0C10.6251 0 12.5899 0.804148 14.1999 2.41244C15.8099 4.02074 16.6137 5.98511 16.6111 8.30556C16.6111 9.24259 16.462 10.1264 16.1639 10.9569C15.8657 11.7875 15.4611 12.5222 14.95 13.1611L23 21.2111L21.2111 23ZM8.30556 14.0556C9.90278 14.0556 11.2606 13.4967 12.3791 12.3791C13.4976 11.2615 14.0564 9.90363 14.0556 8.30556C14.0547 6.70748 13.4959 5.35006 12.3791 4.23328C11.2623 3.1165 9.90448 2.55726 8.30556 2.55556C6.70663 2.55385 5.3492 3.11309 4.23328 4.23328C3.11735 5.35346 2.55811 6.71089 2.55556 8.30556C2.553 9.90022 3.11224 11.2581 4.23328 12.3791C5.35432 13.5001 6.71174 14.059 8.30556 14.0556Z" fill="black"/>
            </svg>
          </button>
        </form>

        <div class="nav">
          <button @click="keywordChange('정치')">정치</button>
          <button @click="keywordChange('사회')">사회</button>
          <button @click="keywordChange('생활문화')">생활문화</button>
          <button @click="keywordChange('세계')">세계</button>
        </div>

        <p>검색창에 키워드를 검색하세요.</p>
      </div>
    </header>

    <swiper
      :slidesPerView="2.2"
      :loop="true"
      :spaceBetween="270"
      :centeredSlides="true"
      :autoplay="{
        delay: 2500,
        disableOnInteraction: false,
      }"
      :pagination="{
        clickable: true,
      }"
      :navigation="true"
      :modules="modules"
      class="mySwiper"
    >
      <swiper-slide v-for="(item, idx) in data" :key="idx" class="slide">
        <a :href="item.link">
          <p class="S_pic"><img :src="item.image" /></p>
          <div class="S_text">
            <b v-html="item.title"></b>
          </div>
        </a>
      </swiper-slide>
    </swiper>

    <ul class="content">
      <li v-for="(item, idx) in data" :key="idx">
        <a :href="item.link">
          <p class="pic"><img :src="item.image" /></p>
          <div class="text">
            <b v-html="item.title"></b>
            <p v-html="item.description"></p>
          </div>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import 'swiper/css';
  import 'swiper/css/pagination';
  import 'swiper/css/navigation';
  import { Autoplay, Pagination, Navigation } from 'swiper/modules';

export default {
  data() {
    return { 
      data: [], 
      keyword: '축구',
      isSearchOpen: false // 검색창 상태 관리 변수
    }
  }, 
  methods: {
    // 1. nav 버튼을 클릭했을 때 실행되는 메서드 수정
    keywordChange(value) {
      this.keyword = value;
      this.newsList();
      this.isSearchOpen = false; // 검색창 닫기 추가
    },
    // 2. 검색창 안에서 엔터를 치거나 돋보기(button)를 눌렀을 때 실행되는 통합 메서드 추가
    handleSearch() {
      this.newsList();
      this.isSearchOpen = false; // 검색창 닫기 추가
    },
    newsList() {      
      fetch(`https://r-todolist.vercel.app/news?keyword=${this.keyword}`)
      .then(res=>res.json())
      .then(res=>{
        this.data = res;      
      })
    }
  },
  mounted() {
    this.newsList()
  },
  name: 'HomeView',
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    return {
      modules: [Autoplay, Pagination, Navigation],
    };
  },
}
</script>

<style>
  body {
    margin: 0;
    padding: 0;  
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: rgb(0 40 133 / 91%);
    color: white;
    font-weight: bold;
    padding: 0 10px;
    position: relative;
  }
  header> svg{
    height: 23px;
  }

  .search{
    background-color: white;
    position: absolute;
    top: 100%; left: 0;
    width: 100%; height: 150px;
    z-index: 999;
  }
  .search> form{
    margin-top: 20px;
    display: inline-flex;
    align-items: center;
    gap: 5px;
    border: 1px solid black;
    padding: 3px 10px;
  }
  .search .search_inp{
    border: none;
    font-size: 14px;
  }
  .search .search_btn{
    background: transparent;
    border: none;
    padding: 0;
  }
  .search> p{
    color: gray;
    font-size: 12px;
    font-weight: 400;
  }

  .nav{
    padding: 10px 0;
  }
  .nav> button:nth-of-type(2){
    border-left: 1px solid black;
    border-right: 1px solid black;
  }
  .nav> button:nth-of-type(3){
    border-right: 1px solid black;
  }
  .nav> button{
    border: none;
    background: white;
  }
  .search{}
  .content{
    
  }
  .content{
    list-style: none;
    padding-left: 0; 
  }
  .content> li> a{
    display: flex;
    align-items: center;
    gap: 20px;
    padding: 0 30px;
    text-decoration: none;  
    color: inherit;   
  }
  .content> li{
  }
  .pic{
    width: 50%; 
    height: 100px;
  }
  .pic >img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .text{ 
    width: 50%;  
    overflow: hidden;      
  }
  .text> b{
    white-space: nowrap;       
    text-overflow: ellipsis;   
    overflow: hidden;      
  }
  .text> p{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;    
    overflow: hidden;     
    font-size: 12px; 
    text-align: left;
  }

  .swiper{padding: 20px 0 10px 0;}
  .swiper-button-prev, .swiper-button-next{
    display: none;
  }
  .slide{}
  .slide> a{
    display: flex;
    flex-direction: column;
    align-items: center;    
    text-decoration: none;
  }
  .S_pic{
    width: 270px;
    height: 150px;
    overflow: hidden;
    border-radius: 10px;
  }
  .S_pic> img{
    width: 100%; height: 100%;
    object-fit: cover;
  }
  .S_text{
    width: 250px;  
    overflow: hidden; 
  }
  .S_text> b{
    white-space: nowrap;       
    text-overflow: ellipsis;   
    overflow: hidden; 
    color: black;
  }
  .swiper-pagination-bullet{
    display: none;
  }
</style>