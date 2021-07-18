<template>
    <div class="grid grid-cols-1 content-center">
        <section>
            <div class="p-2 items-center">
                <div class="inline-block p-5 text-xl">Countdown:</div>
                <div class="inline-block">
                    <input type="text" v-model="user_input_min" placeholder="(Min)" class="px-3 py-3 border-2 border-black w-36 h-12" />
                </div>
                <div class="inline-block px-2"><button @click="convert_to_seconds(user_input_min)" class="bg-green-400 border-4 hover:border-green-400 border-green-400 text-white font-bold py-2 px-4 h-12">START</button></div>
            </div>
        </section>
        <section>
            <div class="p-2">
                <a class="ml-24 italic text-xl">{{ countDownMessage }}</a>
            </div>
        </section>
        <section>
            <a class="inline-block ml-6 text-9xl">{{ display_min }} : {{ display_sec }}</a>
            <div class="inline-block">
                <button @click="start_stop()" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" src="src/assets/pause.png" alt="Play Button" />
                </button>
            </div>
        </section>
        <section>
            <div class="p-2 my-4">
                <div class="inline-block mx-5"><button class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1X</button></div>
                <div class="inline-block mx-5"><button class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1.5X</button></div>
                <div class="inline-block mx-5"><button class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">2X</button></div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: "Countdown",
        props: {},
        data() {
            return {
                countDownMessage: "",
                user_input_min: null,
                user_input_sec: null,
                display_min: "00",
                display_sec: "00",
                stop: false,
            };
        },
        methods: {
            convert_to_seconds(user_input_min) {
                this.user_input_sec = user_input_min * 60;
                this.countdown(this.user_input_sec);
            },
            start_stop() {
                this.stop = true
            },
            countdown(duration) {
                let that = this;
                let timer = duration,
                    minutes,
                    seconds;
                this.countDownMessage = "Count Down Begin!";
                let time = setInterval(function () {
                    minutes = parseInt(timer / 60, 10);
                    seconds = parseInt(timer % 60, 10);
                    that.display_min = String(minutes).padStart(2, "0");
                    that.display_sec = String(seconds).padStart(2, "0");
                    if (--timer < 0 || that.stop == true) {
                        clearInterval(time);
                        that.user_input_min = null
                        that.user_input_sec = null
                        that.stop == false
                    }
                }, 1000);
            },
        },
    };
</script>
