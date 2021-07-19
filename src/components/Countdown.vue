<template>
    <div class="grid grid-cols-1 content-center">
        <section>
            <div class="p-2 items-center">
                <div class="inline-block p-5 text-xl">Countdown:</div>
                <div class="inline-block">
                    <input type="text" v-model="user_input_min" placeholder="(Min)" class="px-3 py-3 border-2 border-black w-36 h-12" />
                </div>
                <div class="inline-block px-2">
                    <button ref="start_button" :disabled="start" @click="start = true, countDownMessage = 'Begin!', min_to_seconds()" class="bg-green-400 border-4 hover:border-green-400 border-green-400 text-white font-bold py-2 px-4 h-12">
                        START
                    </button>
                </div>
            </div>
        </section>
        <section>
            <div v-show="countDownMessage != null" class="w-96 ml-5 bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
                <strong class="font-bold">{{ countDownMessage }}</strong>
            </div>
        </section>
        <section>
            <a :id="blink" :style="{ color: activeColor }" class="inline-block ml-6 text-9xl">{{ display_min }} : {{ display_sec }}</a>
            <div class="inline-block">
                <button v-show="paused == false && start == true" @click="paused = true" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" src="../assets/pause.png" alt="Play Button" />
                </button>
                <button v-show="paused == true && start == true" @click="paused = false, min_to_seconds()" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" src="../assets/play.png" alt="Play Button" />
                </button>
                <button v-show="countDownMessage == 'Stopped!'" @click="refresh()" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" src="../assets/refresh.png" alt="Play Button" />
                </button>
            </div>
        </section>
        <section>
            <div class="p-2 my-4">
                <div class="inline-block mx-5"><button :style="{ backgroundColor: button[0] }" @click="speed_adjust(0)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1X</button></div>
                <div class="inline-block mx-5"><button :style="{ backgroundColor: button[1] }" @click="speed_adjust(1.5)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">1.5X</button></div>
                <div class="inline-block mx-5"><button :style="{ backgroundColor: button[2] }" @click="speed_adjust(2)" class="bg-white-500 border-2 active:bg-gray-400 text-black font-bold py-2 px-4 w-24 h-12">2X</button></div>
            </div>
        </section>
    </div>
</template>

<script>
    export default {
        name: "Countdown",
        data() {
            return {
                countDownMessage: null,
                user_input_sec: null,
                user_input_min: null,
                display_min: "00",
                display_sec: "00",
                count: null,
                speed: 1000,
                paused: false,
                start: false,
                button: [null, null, null],
                activeColor: "black",
                blink: "none",
            };
        },
        methods: {
            min_to_seconds() {
                this.paused == false;
                if (this.count == null) {
                    this.count = this.user_input_min * 60;
                } else {
                    this.count = Math.floor(this.count);
                }
                this.speed = 1000;
                this.timer();
            },
            refresh() {
                window.location.reload();
            },
            speed_adjust(adjust) {
                this.paused = false;
                if (adjust == 1.5) {
                    this.speed = 750;
                    this.button[1] = "#4fd499";
                    this.button[2] = null;
                    this.button[0] = null;
                } else if (adjust == 2) {
                    this.speed = 500;
                    this.button[2] = "#4fd499";
                    this.button[0] = null;
                    this.button[1] = null;
                } else {
                    this.speed = 1000;
                    this.button[0] = "#4fd499";
                    this.button[1] = null;
                    this.button[2] = null;
                }
            },
            timer() {
                this.count--;
                let minutes = parseInt(this.count / 60, 10);
                let seconds = parseInt(this.count % 60, 10);
                this.display_min = String(minutes).padStart(2, "0");
                this.display_sec = String(seconds).padStart(2, "0");
                if (this.count <= 0) {
                    this.countDownMessage = "Stopped!";
                    this.start = false;
                    return;
                }
                let timeout = setTimeout(this.timer, this.speed);
                if (this.paused == true) {
                    window.clearTimeout(timeout);
                } else if (this.count == (this.user_input_min * 60) / 2) {
                    this.countDownMessage = "More then halfway there!";
                } else if (this.count == 20) {
                    this.activeColor = "red";
                } else if (this.count <= 10) {
                    this.blink = "time_text";
                }
            },
        },
    };
</script>
