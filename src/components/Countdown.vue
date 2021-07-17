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
                <button @click="play_pause = !play_pause, start_stop(play_pause)" class="absolute top-40 text-black py-2 px-4">
                    <img id="play" width="62" :src="'src/assets/'+pause_image" alt="Play Button" />
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
                save_time: null,
                pause_image: "pause.png",
                speed: {
                    type: Number,
                    default: 1000,
                },
            };
        },
        methods: {
            convert_to_seconds(user_input_min) {
                this.user_input_sec = user_input_min * 60;
                console.log(this.user_input_sec);
                this.countdown(this.user_input_sec);
            },
            start_stop(pause) {
                console.log(pause)
                let that = this;
                if (pause == false) {
                    that.pause_image = "play.png";
                    let new_duration = this.display_min * 60 + this.display_sec;
                    this.countdown(new_duration);
                } else {
                    that.pause_image = "pause.png";
                    this.save_time = {
                        min: this.display_min,
                        sec: this.display_sec,
                    };
                    console.log(that.countdown)
                    
                }
            },
            countdown(duration) {
                console.log(duration)
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
                    console.log(that.display_min && that.display_sec)
                    if (timer < 0 && --timer < 0) {
                        timer = duration;
                    }else {
                        clearInterval(time)
                        duration = 0
                    }
                }, 1000);
            }, 
        },
    };
</script>
