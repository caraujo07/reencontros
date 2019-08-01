<template>
  <section id="search-bar">
    <input type="text" v-model="busca" placeholder="Busque um vídeo" @input="getVideo()">
    <div v-if="loaded">
     
      <div v-for="res in resultado" :key="res.itag">
        
        <iframe v-for="(id, index) in videoId" :src="id" :key="index" frameborder="0"></iframe>
        
        
      </div>

    </div>
    <button @click=getVideo>buscar vídeo</button>
  </section>
</template>




<script>
export default {
  
  data: function() {
    return {
      videos: {},
      busca: '',
      resultado: [],
      videoId: [], 
      loaded: false
    }
  },
  methods: {
    getVideo() {

      const url = (`https://www.googleapis.com/youtube/v3/search?part=snippet&key=AIzaSyCEmAseUxKNNvU_2M3ip8zYWqSFYXLvvPs&q=${this.busca}&maxResults=10&type=video`);

      // let params = {
      //   part: 'snippet',
      //   key: 'AIzaSyCEmAseUxKNNvU_2M3ip8zYWqSFYXLvvPs',
      //   q: this.busca,
      //   maxResults: 10,
      //   type: 'video'
      // };

      fetch(url)
      .then(r => r.json())
      .then(r => {
        this.videos = r;
        this.resultado = r.items;
        this.videoId = r.items.id.videoId;
        this.loaded = true;
      });

    },
  },
  created() {
    
  }
}
</script>



