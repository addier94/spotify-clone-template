<template>
  <div class="bg-dark h-screen">
    <div class="flex" style="height: 88vh">
      <!-- side nav -->
      <div class="w-56 bg-black h-full flex-none">
        <div class="p-6">
          <img
            :src="imageLogo"
            class="h-10"
            style="filter: brightness(0) invert(1)"
          />
        </div>
        <div class="px-2 mb-5">
          <button
            v-for="page in pages"
            @click="setID = page.id"
            :key="page.id"
            :class="`w-full focus:outline-none text-sm opacity-75 hover:opacity-100 font-semibold rounded px-3 py-2 flex items-center justify-start ${
              setID === page.id ? 'bg-light text-white' : 'text-lightest'
            }`"
          >
            <font-awesome-icon
              class="mr-3 text-lg"
              :icon="['fas', page.icon]"
            />
            <p>{{ page.name }}</p>
          </button>
        </div>
        <div class="mx-5">
          <h1 class="mb-3 text-xs text-lightest tracking-widest uppercase">
            Playlists
          </h1>
          <button
            class="flex items-center justify-start opacity-75 hover:opacity-100 mb-2"
          >
            <font-awesome-icon
              class="bg-white text-3xl p-2 mr-3"
              :icon="['fas', 'plus']"
            />
            <p class="text-sm text-white font-semibold">Create Playlist</p>
          </button>
          <button
            class="flex items-center justify-start opacity-75 hover:opacity-100"
          >
            <font-awesome-icon
              class="bg-blue-400 text-white text-3xl p-2 mr-3"
              :icon="['fas', 'heart']"
            />
            <p class="text-sm text-white font-semibold">Liked Songs</p>
          </button>
          <div class="h-px w-full bg-light my-3"></div>
        </div>
        <div class="mx-5">
          <div class="w-full h-10 overflow-y-scroll">
            <p
              v-for="album in albums"
              :key="album.name"
              class="text-lightest hover:text-white text-xs py-1"
            >
              {{ album.name }}
            </p>
          </div>
          <button
            class="flex items-center justify-start text-lightest hover:text-white py-2"
          >
            <font-awesome-icon
              class="mr-3 rounded-full border text-sm border-lightest"
              :icon="['fas', 'arrow-down']"
            ></font-awesome-icon>
            <p>Install App</p>
          </button>
        </div>
        <div class="relative pt-4">
          <div
            class="w-full h-full flex justify-end items-start opacity-0 hover:opacity-100 p-2 absolute"
          >
            <div
              class="bg-black rounded-full h-6 w-6 flex items-center justify-center"
            >
              <font-awesome-icon
                class="text-white"
                :icon="['fas', 'check']"
              ></font-awesome-icon>
            </div>
          </div>
          <img :src="advertisingImage" />
        </div>
      </div>
      <!-- main content -->
      <div class="w-full h-full relative overflow-y-scroll">
        <!-- header -->
        <div
          class="w-full sticky top-0 py-4 px-6 flex items-center justify-between"
        >
          <div class="flex items-center">
            <button class="rounded-full bg-black w-8 h-8 text-white mr-3">
              <font-awesome-icon
                :icon="['fas', 'chevron-left']"
              ></font-awesome-icon>
            </button>
            <button class="rounded-full bg-black w-8 h-8 text-white">
              <font-awesome-icon
                :icon="['fas', 'chevron-right']"
              ></font-awesome-icon>
            </button>
          </div>
          <div class="relative">
            <button
              @click="showDropdown = !showDropdown"
              class="bg-light rounded-full p-1 px-2 flex items-center focus:outline-none"
            >
              <img :src="myProfilePhoto" class="rounded-full h-6 w-6 mr-2" />
              <p class="text-white font-semibold text-xs mr-3">
                Alfredo Fernandez
              </p>
              <font-awesome-icon
                v-if="showDropdown === false"
                class="text-white mx-1"
                :icon="['fas', 'caret-down']"
              ></font-awesome-icon>
              <font-awesome-icon
                v-if="showDropdown === true"
                class="text-white mx-1"
                :icon="['fas', 'caret-up']"
              ></font-awesome-icon>
            </button>
            <div
              v-if="showDropdown === true"
              class="absolute bg-light w-full rounded mt-1"
            >
              <button
                @click="showDropdown = false"
                class="focus:outline-none w-full text-sm py-2 text-lightest border-b border-whiten opacity-75 hover:opacity-100"
              >
                Account
              </button>
              <button
                @click="showDropdown = false"
                class="focus:outline-none w-full text-sm py-2 text-lightest border-b border-light opacity-75 hover:opacity-100"
              >
                Log Out
              </button>
            </div>
          </div>
        </div>
        <!-- cards -->
        <div class="px-6 py3 mb-4">
          <div class="flex items-center justify-between">
            <h1
              class="pl-2 text-2xl font-semibold text-white tracking-wide hover:underline"
            >
              Recently Posts Played
            </h1>
            <h2
              class="pr-8 pt-4 text-xs text-lightest uppercase tracking-wide hover:underline mb-3"
            >
              See All
            </h2>
          </div>
          <div class="w-full flex flex-wrap">
            <div
              v-for="recent in recents"
              :key="recent"
              class="p-2 w-48 relative"
            >
              <div
                class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100"
              >
                <div
                  class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
                >
                  <font-awesome-icon
                    :icon="['fas', 'play']"
                    class="text-white"
                  ></font-awesome-icon>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${recent.src}`" class="h-auto w-full shadow mb-2" />
                <h1 class="text-sm font-semibold text-white tracking-wide">
                  {{ recent.title }}
                </h1>
                <h2 class="text-xs text-lightest tracking-wide pb-5">
                  {{ recent.artist }}
                </h2>
              </div>
            </div>
          </div>
        </div>
        <div class="px-6 py3">
          <div class="pl-2">
            <h1
              class="text-2xl font-semibold text-white tracking-wide hover:underline"
            >
              Made for Stephanie
            </h1>
            <h2 class="text-sm text-lightest">
              Get better recommendations the more you listen.
            </h2>
          </div>
          <div class="w-full flex flex-wrap">
            <div
              v-for="recent in recents"
              :key="recent"
              class="p-2 w-48 relative"
            >
              <div
                class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100"
              >
                <div
                  class="bg-green rounded-full h-10 w-10 flex items-center justify-center"
                >
                  <font-awesome-icon
                    :icon="['fas', 'play']"
                    class="text-white"
                  ></font-awesome-icon>
                </div>
              </div>
              <div class="bg-light w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${recent.src}`" class="h-auto w-full shadow mb-2" />
                <h1 class="text-sm font-semibold text-white tracking-wide">
                  {{ recent.title }}
                </h1>
                <h2 class="text-xs text-lightest tracking-wide pb-5">
                  {{ recent.artist }}
                </h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- play bar -->
    <div
      class="w-full flex items-center justify-between px-3 bg-light"
      style="height: 12vh"
    >
      <div class="flex items-center w-1/4">
        <div>
          <h1 class="text-sm text-white tracking-wide">
            Summer in the City - Remastered
          </h1>
          <h2 class="text-xs text-lightest tracking-wide">
            The Lovin' Spoonfull
          </h2>
        </div>
        <font-awesome-icon
          class="text-xl text-green mx-4"
          :icon="['fas', 'heart']"
        ></font-awesome-icon>
        <font-awesome-icon
          class="text-xl text-lightest hover:text-white"
          :icon="['fas', 'image']"
        ></font-awesome-icon>
      </div>
      <div class="flex flex-col justify-center w-2/4 items-center">
        <div class="flex items-center">
          <button class="mx-5 text-lightest hover:text-white">
            <font-awesome-icon
              class="text-lg"
              :icon="['fas', 'random']"
            ></font-awesome-icon>
          </button>
          <button class="text-lightest hover:text-white">
            <font-awesome-icon
              class="text-lg"
              :icon="['fas', 'backward']"
            ></font-awesome-icon>
          </button>
          <button
            @click.prevent="playSong('song.mp3'), (pause = true)"
            class="rounded-full h-8 w-8 flex items-center justify-center mx-5 border-lightest border text-lightest hover:text-white"
          >
            <font-awesome-icon
              v-if="pause === false"
              class="text-lg"
              :icon="['fas', 'play']"
            ></font-awesome-icon>
            <font-awesome-icon
              v-if="pause === true"
              class="text-lg"
              :icon="['fas', 'pause-circle']"
            ></font-awesome-icon>
          </button>
          <button class="text-lightest hover:text-white">
            <font-awesome-icon
              class="text-lg"
              :icon="['fas', 'forward']"
            ></font-awesome-icon>
          </button>
          <button class="mx-5 text-lightest hover:text-white">
            <font-awesome-icon
              class="text-lg"
              :icon="['fas', 'redo']"
            ></font-awesome-icon>
          </button>
        </div>
        <div class="w-3/4 flex items-center mt-3">
          <p class="text-xs text-lightest mr-1">0:29</p>
          <div class="w-full h-1 bg-dark rounded-full flex items-center">
            <div class="h-1 rounded-full bg-green" style="width: 18%"></div>
            <div class="h-3 w-3 bg-white rounded-full -ml-1 shadow"></div>
          </div>
          <p class="text-xs text-lightest ml-1">2:40</p>
        </div>
      </div>
      <div class="flex items-center w-1/4 justify-end">
        <font-awesome-icon
          class="text-lightest hover:text-white"
          :icon="['fas', 'sliders-h']"
        ></font-awesome-icon>
        <font-awesome-icon
          class="text-xl text-lightest mx-3 hover:text-white"
          :icon="['fas', 'receipt']"
        ></font-awesome-icon>
        <font-awesome-icon
          class="text-xl text-lightest hover:text-white"
          :icon="['fas', 'volume-up']"
        ></font-awesome-icon>
        <div class="w-20 ml-1 bg-lightest rounded-full h-1"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      advertisingImage:
        "https://soymarketing.gumlet.io/wp-content/uploads/2016/03/vintage.png?compress=true&quality=80&w=720&dpr=2.6",
      myProfilePhoto:
        "https://lh3.googleusercontent.com/a-/AOh14Ggn9AHEKty0W-5MIz8k3hcqcpbu-Ix6Ylv2HVDQ3w=s96-c-rg-br100",
      imageLogo:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Spotify_logo_with_text.svg/1200px-Spotify_logo_with_text.svg.png",
      pages: [
        { id: "home", name: "Home", icon: "home" },
        { id: "search", name: "Search", icon: "search" },
        { id: "library", name: "Your Library", icon: "chart-bar" },
      ],
      setID: "home",
      albums: [
        { name: "drive" },
        { name: "zhu" },
        { name: "All New Indie" },
        { name: "Mellow" },
        { name: "Classic Road Trip Songs" },
        { name: "Lana Del Rey Radio" },
      ],
      showDropdown: false,
      recents: [
        {
          src:
            "https://as01.epimg.net/epik/imagenes/2019/12/03/portada/1575384297_599943_1575384448_noticia_normal_recorte1.jpg",
          title: "Daily Mix 2",
          artist: "By Spotify",
        },
        {
          src:
            "https://happyfm.es/wp-content/uploads/2019/01/por-que-sebastian-yatra-es-uno-de-los-artistas-mas-importantes-de-nuestra-generacion-01-700x394.jpg",
          title: "Daily Mix 3",
          artist: "By Spotify",
        },
        {
          src:
            "https://www.eluniverso.com/sites/default/files/styles/powgallery_1024/public/fotos/2019/10/ozuna_0.jpg?itok=B6EZwa-P",
          title: "Billie Eilish Radio",
          artist: "Billie Eilish",
        },
        {
          src:
            "https://www.lavanguardia.com/r/GODO/LV/p6/WebSite/2019/02/10/Recortada/_20190209061825354-keAD-U46337372325r1B-992x558@LaVanguardia-Web.jpg",
          title: "Cold Case Files",
          artist: "PodcastOne",
        },
        {
          src:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSOsqgUgKop8RyykgyhPc8FhMm_wIE_0jDefQ&usqp=CAU",
          title: "Life Is Good Radio",
          artist: "By Spotify",
        },
        {
          src:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRNhPHvZyKJdRZEa675wV-f-l7M2KeMxh5W0w&usqp=CAU",
          title: "run",
          artist: "Stephanie Dietz",
        },
      ],
      pause: false,
    };
  },
  methods: {
    playSong(song) {
      if (song) {
        let audio = new Audio(song);
        audio.play();
      }
    },
  },
};
</script>

<style src="@/assets/styles/main.css">
</style>

