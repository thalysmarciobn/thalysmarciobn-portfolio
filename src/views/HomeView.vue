<script>

import axios from 'axios';

import _data from '../data.json'

export default {
  name: 'HomeView',
  data() {
    return { 
      linkedin: _data.linkedin,
      github: _data.github,
      discord_status: '',
      discord_user: {
        id: -1,
        username: 'Carregando...'
      }
    }
  },
  mounted() {
    axios.get(`https://api.lanyard.rest/v1/users/${_data.discordId}`).then((data) => {
      const res = data.data.data
      console.log(data)
      this.discord_status = res.discord_status
      this.discord_user = res.discord_user

      const socket = new WebSocket('wss://api.lanyard.rest/socket')
      socket.addEventListener('open', () => {
        socket.send(
          JSON.stringify({ op: 2, d: { subscribe_to_id: _data.discordId } })
        )
        setInterval(() => {
          socket.send(JSON.stringify({ op: 3 }))
        }, 30000)
      })
      socket.addEventListener("message", ({ data }) => {
      var _d = JSON.parse(data)
        if(_d.op === 0) {
          const res = _d.d
          this.discord_status = res.discord_status
          this.discord_user = res.discord_user
        }
      })
    })
  },
  components: {
  }
}
</script>

<template>
  <section class="h-full">
    <div class="h-screen bg-gray-200 w-full grid place-items-center">
      <div class="py-8 px-4 mx-auto max-w-screen-xl text-center z-10 relative">
        <h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none md:text-5xl lg:text-6xl text-white">
          Olá, me chamo Thalys
        </h1>
        <p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 lg:px-48 text-gray-200">
          Um desenvolvedor Full Stack que ama experimentar e aprender coisas novas.
        </p>
        <router-link :to="{ name: 'gallery' }" class="relative inline-flex items-center justify-center mt-10 mb-10 h-16 px-10 py-0 text-xl font-semibold text-center text-gray-200 no-underline align-middle transition-all duration-300 ease-in-out bg-transparent border-2 border-gray-600 border-solid rounded-full cursor-pointer select-none hover:text-white hover:border-white focus:shadow-xs focus:no-underline">
          <svg class="w-9 h-7 mr-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="32" height="32" id="pencil"><path style="isolation:auto;mix-blend-mode:normal" d="M27.5 1044.862c0 1.108-.892 2-2 2h-21c-1.108 0-2-.892-2-2zM4.5 1031.862h21v13h-21z" color="#000" opacity=".15" overflow="visible" transform="translate(.5 -1018.862)"></path><path fill="#2b4255" color="#000" overflow="visible" style="isolation:auto;mix-blend-mode:normal" d="M5.5 1031.862h21v13h-21z" transform="translate(.5 -1018.862)"></path><path style="isolation:auto;mix-blend-mode:normal" fill="#4bbfeb" d="M6.5 1032.862h19v11h-19z" color="#000" overflow="visible" transform="translate(.5 -1018.862)"></path><path fill="#576d7e" d="M28.5 1044.862c0 1.108-.892 2-2 2h-21c-1.108 0-2-.892-2-2z" color="#000" overflow="visible" style="isolation:auto;mix-blend-mode:normal" transform="translate(.5 -1018.862)"></path><path fill="#cad1d8" d="M18.5 1044.862c0 .277-.223.5-.5.5h-4a.499.499 0 0 1-.5-.5" color="#000" overflow="visible" style="isolation:auto;mix-blend-mode:normal" transform="translate(.5 -1018.862)"></path><path d="M23-1043.862v18.5c0 .554-.446 1-1 1h-4c-.554 0-1-.446-1-1v-18.5z" color="#000" opacity=".15" overflow="visible" transform="matrix(1 0 0 -1 .5 -1018.862)" style="isolation:auto;mix-blend-mode:normal"></path><path fill="#f05542" d="M24-1043.862v18.5c0 .554-.446 1-1 1h-4c-.554 0-1-.446-1-1v-18.5z" color="#000" overflow="visible" transform="matrix(1 0 0 -1 .5 -1018.862)" style="isolation:auto;mix-blend-mode:normal"></path><path fill="none" stroke="#34485c" d="M18.5 23.453h1m-1-2h2m-2-2h1m-1-2h2m-2-2h1m-1-2h2m-2-2h1m-1-2h2m-2-2h1"></path><path fill="#f17f53" d="M-1043.862-23h19.5v1h-19.5z" color="#000" overflow="visible" transform="matrix(0 -1 -1 0 .5 -1018.862)" style="isolation:auto;mix-blend-mode:normal"></path><path style="isolation:auto;mix-blend-mode:normal" d="m13 5-2 4v14.5h4V9Z" color="#000" opacity=".15" overflow="visible" transform="translate(.5 1.5)"></path><path fill="#f05542" d="M12-1043.862h4v14.5h-4z" color="#000" overflow="visible" transform="matrix(1 0 0 -1 .5 -1018.862)" style="isolation:auto;mix-blend-mode:normal"></path><path fill="#e9eded" d="M12 1029.362h4l-2-4z" color="#000" overflow="visible" style="isolation:auto;mix-blend-mode:normal" transform="translate(.5 -1018.862)"></path><path fill="none" stroke="#34485c" d="M14.5 10.5V25"></path><path fill="#34485c" d="m13.5 1026.362.5-1 .5 1h-1z" color="#000" overflow="visible" style="isolation:auto;mix-blend-mode:normal" transform="translate(.5 -1018.862)"></path></svg>
            <span class="w-full">Acessar Galeria</span>
            <svg class="w-3.5 h-3.5 ml-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
          </svg>
        </router-link> 

        <ul role="list" class="w-full max-w-md mx-auto divide-y divide-gray-200 divide-gray-700">
          <li class="py-3 sm:py-4">
            <a :href="`https://discordapp.com/users/${discord_user.id}`" target="_blank">
              <div class="px-3.5 py-2.5 bg-gray-900 rounded-full">
                <div class="relative flex items-center">
                  <div class="flex-shrink-0 transition duration-700 ease-in-out">
                      <img class="w-8 h-8 rounded-full" :src="discord_user.id == -1 ? 
                        'assets/discord.png' : `https://cdn.discordapp.com/avatars/${discord_user.id}/${discord_user.avatar}.png`">
                  </div>
                  <div class="flex-1 min-w-0">
                    <p class="text-sm font-semibold truncate text-white">
                      {{ discord_user.username }}
                    </p>
                  </div>
                  <span :class="{
                      'bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-300': discord_status === 'idle',
                      'bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-300': discord_status === 'online',
                      'bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-300': discord_status === 'dnd' || discord_status === 'offline',
                      'bg-gray-100 text-gray-800 dark:bg-gray-900 dark:text-gray-300': discord_status === '...'
                    }"
                    class="absolute right-0 transition duration-700 ease-in-out inline-flex items-center text-xs font-medium w-25 mr-2 px-2.5 py-0.5 rounded-full">
                    <span
                      class="w-2 h-2 mr-1 rounded-full"
                      :class="{
                        'bg-yellow-500': discord_status === 'idle',
                        'bg-green-500': discord_status === 'online',
                        'bg-red-500': discord_status === 'dnd' || discord_status === 'offline',
                      }"
                    ></span>
                    {{ discord_status }}
                  </span>
                </div>
              </div>
            </a>
          </li>
        </ul>
        <div class="mt-10 mb-5">
          <div class="flex flex-wrap justify-center gap-2">
            <a :href="linkedin" target="_blank" class="bg-blue-600 p-2 font-semibold text-white inline-flex items-center space-x-2 rounded">
              <svg class="w-5 h-5 fill-current" role="img" viewBox="0 0 256 256" xmlns="http://www.w3.org/2000/svg">
                <g><path d="M218.123122,218.127392 L180.191928,218.127392 L180.191928,158.724263 C180.191928,144.559023 179.939053,126.323993 160.463756,126.323993 C140.707926,126.323993 137.685284,141.757585 137.685284,157.692986 L137.685284,218.123441 L99.7540894,218.123441 L99.7540894,95.9665207 L136.168036,95.9665207 L136.168036,112.660562 L136.677736,112.660562 C144.102746,99.9650027 157.908637,92.3824528 172.605689,92.9280076 C211.050535,92.9280076 218.138927,118.216023 218.138927,151.114151 L218.123122,218.127392 Z M56.9550587,79.2685282 C44.7981969,79.2707099 34.9413443,69.4171797 34.9391618,57.260052 C34.93698,45.1029244 44.7902948,35.2458562 56.9471566,35.2436736 C69.1040185,35.2414916 78.9608713,45.0950217 78.963054,57.2521493 C78.9641017,63.090208 76.6459976,68.6895714 72.5186979,72.8184433 C68.3913982,76.9473153 62.7929898,79.26748 56.9550587,79.2685282 M75.9206558,218.127392 L37.94995,218.127392 L37.94995,95.9665207 L75.9206558,95.9665207 L75.9206558,218.127392 Z M237.033403,0.0182577091 L18.8895249,0.0182577091 C8.57959469,-0.0980923971 0.124827038,8.16056231 -0.001,18.4706066 L-0.001,237.524091 C0.120519052,247.839103 8.57460631,256.105934 18.8895249,255.9977 L237.033403,255.9977 C247.368728,256.125818 255.855922,247.859464 255.999,237.524091 L255.999,18.4548016 C255.851624,8.12438979 247.363742,-0.133792868 237.033403,0.000790807055"></path></g>
              </svg>
            </a>

            <a :href="github" target="_blank" class="bg-gray-700 p-2 font-semibold text-white inline-flex items-center space-x-2 rounded">
              <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" class="w-5" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24">
                <g fill="none"><path fill-rule="evenodd" clip-rule="evenodd" d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385c.6.105.825-.255.825-.57c0-.285-.015-1.23-.015-2.235c-3.015.555-3.795-.735-4.035-1.41c-.135-.345-.72-1.41-1.23-1.695c-.42-.225-1.02-.78-.015-.795c.945-.015 1.62.87 1.845 1.23c1.08 1.815 2.805 1.305 3.495.99c.105-.78.42-1.305.765-1.605c-2.67-.3-5.46-1.335-5.46-5.925c0-1.305.465-2.385 1.23-3.225c-.12-.3-.54-1.53.12-3.18c0 0 1.005-.315 3.3 1.23c.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23c.66 1.65.24 2.88.12 3.18c.765.84 1.23 1.905 1.23 3.225c0 4.605-2.805 5.625-5.475 5.925c.435.375.81 1.095.81 2.22c0 1.605-.015 2.895-.015 3.3c0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z" fill="currentColor" /></g>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
