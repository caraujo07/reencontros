<template>
  <section id="search-bar">
    <input type="text" v-model="busca" placeholder="Busque um vídeo">
    <div v-if="loaded">
     
      <ul>
        <li v-for="(valor, chave, index) in videoId" :key="index">
          <h1>{{valor.video.title}}</h1>
          <iframe width="560" height="315" :src="valor.video.link" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </li>
      </ul>

    </div>
    <button @click="getVideo">buscar vídeo</button>
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

      const url = (`https://www.googleapis.com/youtube/v3/playlistItems?part=snippet&key=AIzaSyCEmAseUxKNNvU_2M3ip8zYWqSFYXLvvPs&playlistId=PLHz_AreHm4dksnH2jVTIVNviIMBVYyFnH&maxResults=50`);

      // let params = {
      //   part: 'snippet',
      //   key: 'AIzaSyCEmAseUxKNNvU_2M3ip8zYWqSFYXLvvPs',
      //   q: this.busca,
      //   maxResults: 10,
      //   type: 'video'
      //   playlistid curso em video python = PLHz_AreHm4dksnH2jVTIVNviIMBVYyFnH
      // };

      fetch(url)
      .then(r => r.json())
      .then(r => {
        this.videos = r;
        this.resultado = r.items;
        this.resultado.forEach((item) => {
          this.videoId.push({"video": {"title": item.snippet.title, "link":"https://www.youtube.com/embed/" + item.snippet.resourceId.videoId}});
        });
        this.loaded = true;
      });

    },
  },
  created() {
    
  }
}
</script>



