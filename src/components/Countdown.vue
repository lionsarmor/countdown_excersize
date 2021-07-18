<template>
    <div class="grid grid-cols-1 content-center">
        <section>
            <div class="p-2 items-center">
                <div class="inline-block p-5 text-xl">Countdown:</div>
                <div class="inline-block">
                    <input type="text" v-model="user_input_min" placeholder="(Min)" class="px-3 py-3 border-2 border-black w-36 h-12" />
                </div>
                <div class="inline-block px-2"><button @click="min_to_seconds()" class="bg-green-400 border-4 hover:border-green-400 border-green-400 text-white font-bold py-2 px-4 h-12">START</button></div>
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
                <button @click="pause_switch()" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" src="src/assets/pause.png" alt="Play Button" />
                </button>
            </div>
        </section>
        <section>
            <div class="p-2 my-4">
                <div class="inline-block mx-5"><button @click="speed_adjust(0)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1X</button></div>
                <div class="inline-block mx-5"><button @click="speed_adjust(1.5)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1.5X</button></div>
                <div class="inline-block mx-5"><button @click="speed_adjust(2)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">2X</button></div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: "Countdown",
        data() {
            return {
                countDownMessage: "",
                user_input_sec: null,
                user_input_min: null,
                display_min: "00",
                display_sec: "00",
                count: null,
                speed: 1000,
                pause: false,
            };
        },
        methods: {
            min_to_seconds() {
                this.pause == false
                this.count = this.user_input_min * 60
                this.timer();
            },
            speed_adjust(adjust) {
                console.log("pressed");
                if (adjust == 1.5) {
                    this.speed = 750;
                } else if (adjust == 2) {
                    this.speed = 500;
                } else {
                    this.speed = 1000;
                }
            },
            pause_switch() {
                this.user_input_min = null
                this.pause = true;
            },
            timer() {
                this.count--;
                console.log(this.count);
                let minutes = parseInt(this.count / 60, 10);
                let seconds = parseInt(this.count % 60, 10);
                this.display_min = String(minutes).padStart(2, "0");
                this.display_sec = String(seconds).padStart(2, "0");
                if (this.count < 1) {
                    return;
                }
                let timeout = setTimeout(this.timer, this.speed);
                if (this.pause == true) {
                    clearTimeout(timeout);
                }
            },
        },
    };
</script>
