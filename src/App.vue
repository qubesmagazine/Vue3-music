<template>

  <div id="app">
    <header>
    <nav>
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Services</a>
</nav>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
    <footer class="footer">
  <p>&copy; 2023 Okwudili Music website. All rights reserved.</p>
</footer>
  </div>
</template>

<script>
export default {

  name: 'app',
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Fake friends',
          artist: 'Yemi Alade',
          src: "../src/assets/Yemi_Alade_-_Fake_Friends_Ir_re__Loadedsongs.com.mp3" ,
        },
        {
          title: 'Peace of Mind',
          artist: 'Teckno',
          src: '../src/assets/Tekno_-_Peace_Of_Mind_Loadedsongs.com.mp3',
        },
        {
          title: 'Loju',
          artist: 'Spinal Ft Wizkid',
          src: '../src/assets/Spinall_ft_Wizkid_-_Loju_Loadedsongs.com.mp3',
        },
        {
          title: 'DND',
          artist: 'Bella Shmurda ft Lil Kesh',
          src: '../src/assets/Bella_Shmurda_ft_Lil_Kesh_-_DND_Loadedsongs.com.mp3',
        },{
          title: 'Sitting on top of the world',
          artist: 'Burna boy ft Tiwa Savage',
          src: '../src/assets/Burna_Boy_ft_21_Savage_-_Sittin_On_Top_Of_The_World_Remix__Loadedsongs.com.mp3',
        },{
          title: 'For You',
          artist: 'Spyro ft Daimond Teni Iyanya',
          src: '../src/assets/Spyro_ft_Diamond_Platnumz_Teni_Iyanya_-_For_You_Loadedsongs.com.mp3',
        },{
          title: 'Ojaginger',
          artist: 'Kcee',
          src: '../src/assets/Kcee_-_Ojaginger_Loadedsongs.com.mp3',
        },
        {
          title: 'Your Body',
          artist: 'Savage',
          src: '../src/assets/Savage_-_Your_Body_Loadedsongs.com.mp3',
        },
        {
          title: 'Lava Lava',
          artist: 'Diamond Platnumz and Tuna',
          src: '../src/assets/Lava_Lava_ft_Diamond_Platnumz_-_Tuna_Kikao_Loadedsongs.com.mp3',
        },
        {
          title: 'Story of Silent',
          artist: 'Tega Boi Dc ft Jaylien',
          src: '../src/assets/Tega_Boi_Dc_ft_Jaylien_-_Story_Of_Silent_Loadedsongs.com.mp3',
        },
        {
          title: 'Wheels on the Bus',
          artist: 'DJ CORA ft HAPPY',
          src: '../src/assets/DJ_CORA_ft_HAPPY_-_Wheels_On_The_Bus_Loadedsongs.com.mp3',
        },
        {
          title: 'Ex Convict',
          artist: 'Shallipopi',
          src: '../src/assets/Shallipopi_-_Ex_Convict_Loadedsongs.com (1).mp3',
        },
        {
          title: 'Kolapia',
          artist: 'Kolaboy ft Ojadili',
          src: '../src/assets/Kolaboy_ft_Ojadili_Igbo_-_Kolapiano_Vol_2_Isakaba__Loadedsongs.com.mp3',
        },
        {
          title: 'Remember Me',
          artist: 'Laycon',
          src: '../src/assets/Laycon_-_Remember_Me_Loadedsongs.com.mp3',
        },
        {
          title: 'My Baby',
          artist: 'Bien ft Franglish Ayra Starr',
          src: '../src/assets/Bien_ft_Franglish_Ayra_Starr_-_My_Baby_Remix__Loadedsongs.com.mp3',
        },
        {
          title: 'Balloranking',
          artist: 'Brand',
          src: '../src/assets/Balloranking_-_Brand_New_Loadedsongs.com.mp3',
        },
        {
          title: 'WurID',
          artist: 'Sarz',
          src: '../src/assets/WurlD_ft_Sarz_-_Location_Loadedsongs.com.mp3',
        },

      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if (typeof song.src != 'undefined') {
        this.current = song

        this.player.src = this.current.src
      }

      this.player.play()
      this.player.addEventListener(
        'ended',
        function () {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0
          }
          this.current = this.songs[this.index]
          this.play(this.current)
        }.bind(this)
      )
      this.isPlaying = true
    },

    pause() {
      this.player.pause()
      this.isPlaying = false
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    },
    prev() {
      this.index--
      if (this.index < 0) {
        this.index = this.songs.lenght - 1
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    }
  },
  created() {
    this.current = this.songs[this.index]
    this.player.src = this.current.src
    this.player.play()
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #000;
  animation: shining 5s infinite, rolling 10s infinite;
}

@keyframes shining {
  0% {
    background-color: #000;
  }
  50% {
    background-color: #fff;
  }
  100% {
    background-color: #000;
  }
}

@keyframes rolling {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 100% 50%;
  }
}

header {
  background-color: rgb(29, 22, 22);
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
}

header nav {
  display: flex;
  gap: 50px;
}

header nav a {
  color: white;
  text-decoration: none;
  font-size: 20px;
  font-style: oblique;
  
}

header nav a:hover {
  text-decoration: underline;
}


main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title, span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}

.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #6b2ecc;
}

.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #58a3ff;
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #ff5858;
}

.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}

.footer {
  background-color: darkred;
  color: #fff;
  padding: 20px;
  text-align: center;
}

.footer .social-icons {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.footer .social-icons a {
  display: inline-block;
  margin: 0 10px;
  color: #fff;
  font-size: 20px;
  text-decoration: none;
}

.footer .social-icons a:hover {
  color: #ff8080;
}

</style>
