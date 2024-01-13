<script setup>


const prop = defineProps({
    data: Object,
    isVisible: Boolean
})

const emit = defineEmits(['isClose'])

const close = () => {
    emit('isClose')
}

const ClickeOutside = (e) => {
    const target = e.target;
    if (target.className == "main") {
        close()
    }
}


</script>

<template>
    <div class="main" @click="ClickeOutside" v-if="isVisible">

        <div id="container">
            <div class="flex justify-end items-end translate-y-[-100%]" >
                <svg class=" cursor-pointer duration-200 hover:text-gray-500" @click="close" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M20 6.91L17.09 4L12 9.09L6.91 4L4 6.91L9.09 12L4 17.09L6.91 20L12 14.91L17.09 20L20 17.09L14.91 12z"/></svg>
            </div>
            <div class="flex md:flex-row flex-col justify-between px-[2rem] pb-[2rem] gap-9">
                <div class="left md:w-[70%] min-w-[20rem] w-full items-center">
                    <img :src="data.flags.png" alt="">
                    <div class="flags-alt p-4 " v-if="data.flags.alt">
                        <h1 class="font-semibold text-xl mb-2">Descriptions</h1>
                        <p class="ml-2">
                            {{ data.flags.alt }}
                        </p>
                    </div>
                </div>

                <div class="right">
                    <h1 class="font-bold text-2xl mb-4 whitespace-nowrap">{{ data.name.official }}</h1>
                    <p class="mb-2">
                        <template v-for="(continent, index) in data.continents">
                            <template v-if="index > 0">
                                ,
                            </template>
                            {{ continent }}
                        </template>
                    </p>
                    <div class="flex items-start mb-2">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                            <path fill="currentColor"
                                d="M12 21q-1.858 0-3.5-.71t-2.86-1.93q-1.22-1.217-1.93-2.86Q3 13.858 3 12q0-1.863.71-3.503q.711-1.64 1.93-2.858Q6.857 4.421 8.5 3.711Q10.142 3 12 3q1.863 0 3.503.71q1.64.711 2.858 1.93q1.218 1.218 1.928 2.857Q21 10.137 21 12q0 1.858-.71 3.5t-1.93 2.86q-1.218 1.219-2.857 1.93Q13.863 21 12 21m0-.992q.88-1.131 1.452-2.221q.571-1.09.929-2.44H9.619q.396 1.426.948 2.516q.552 1.09 1.433 2.145m-1.273-.15q-.7-.825-1.278-2.04q-.578-1.214-.86-2.472H4.753q.86 1.866 2.437 3.06q1.578 1.194 3.536 1.452m2.546 0q1.958-.258 3.536-1.452t2.437-3.06h-3.834q-.38 1.277-.957 2.492q-.578 1.214-1.182 2.02m-8.927-5.512H8.38q-.114-.615-.16-1.199q-.048-.584-.048-1.147q0-.563.047-1.147q.047-.584.16-1.2H4.347q-.163.52-.255 1.133T4 12q0 .602.091 1.214q.092.613.255 1.132m5.035 0h5.238q.114-.615.16-1.18q.048-.564.048-1.166t-.047-1.166q-.047-.565-.16-1.18H9.38q-.113.615-.16 1.18q-.047.564-.047 1.166t.047 1.166q.047.565.16 1.18m6.24 0q1.958-.258 3.536-1.452t2.437-3.06h-3.834q-.879-1.904-2.408-3.06q-1.53-1.156-3.565-1.47q.7.92 1.259 2.106q.558 1.185.88 2.424m-5.793 0h4.762q-.396-1.408-.977-2.546q-.58-1.139-1.404-2.116q-.823.977-1.404 2.116q-.58 1.138-.977 2.546m-4.865 0h3.834q.322-1.239.88-2.424q.559-1.186 1.259-2.107q-2.054.315-3.574 1.48q-1.52 1.166-2.4 3.05" />
                        </svg>
                        <div class="flex flex-col  justify-start">

                            <p v-for="(value, key) in data.languages" :key="key" class="ml-2 capitalize ">
                                {{ key }} : {{ value }}
                            </p>
                        </div>

                    </div>

                    <div class="flex flex-col items-start mb-4">
                        <!-- Country Codes -->
                        <div class="flex items-center mb-2">
                            <span class="font-semibold mr-2">cca2:</span>
                            <p>{{ data.cca2 }}</p>
                        </div>

                        <div class="flex items-center">
                            <span class="font-semibold mr-2">cca3:</span>
                            <p>{{ data.cca3 }}</p>
                        </div>
                    </div>

                    <div class="flex items-start mb-2">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                            <path fill="currentColor"
                                d="M12 14c2.206 0 4-1.794 4-4s-1.794-4-4-4s-4 1.794-4 4s1.794 4 4 4m0-6c1.103 0 2 .897 2 2s-.897 2-2 2s-2-.897-2-2s.897-2 2-2" />
                            <path fill="currentColor"
                                d="M11.42 21.814a.998.998 0 0 0 1.16 0C12.884 21.599 20.029 16.44 20 10c0-4.411-3.589-8-8-8S4 5.589 4 9.995c-.029 6.445 7.116 11.604 7.42 11.819M12 4c3.309 0 6 2.691 6 6.005c.021 4.438-4.388 8.423-6 9.73c-1.611-1.308-6.021-5.294-6-9.735c0-3.309 2.691-6 6-6" />
                        </svg>
                        <div class="flex flex-col items-start">
                            <p v-for="(value, key) in data.maps" :key="key" class="ml-2">
                                {{ key }} : {{ value }}
                            </p>
                        </div>

                    </div>
                    <div class="nativeName">
                        <div class="flex flex-col items-start">
                            <p class="ml-2">
                                <template v-for="(name, key) in data.name.nativeName.eng" :key="key">

                                    <p><span class=" capitalize">{{ key }}</span> : {{ name }}</p>
                                </template>
                            </p>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<style lang="scss" scoped>
 .main {
     width: 100vw;
     height: 100vh;
     background-color: #edede96f;
     font-family: 'Sono', sans-serif;
     position: fixed;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
     z-index: 10000000;

     #container {
         // width: max-content;
         background-color: rgb(243, 241, 241);
         overflow: auto;
         max-height: 100vh;
         // opacity: 1 !important;
         position: fixed;
         z-index: 1000;
         padding: .7rem;
         padding-top: 2rem;
         top: 50%;
         left: 50%;
         transform: translate(-50%, -50%);
        @media only screen and (width < 780px) {
            top: 0%;
            transform: translate(-50%, 0);
        }



     }
 }
</style>