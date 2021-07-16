<template>
    <div class="grid grid-cols-1 content-center">
        <section>
            <div class="p-2 items-center">
                <div class="inline-block p-5 text-xl">Countdown:</div>
                <div class="inline-block">
                    <input type="text" placeholder="(Min)" class="px-3 py-3 border-2 border-black w-36 h-12" />
                </div>
                <div class="inline-block px-2"><button class="bg-green-400 border-4 hover:border-green-400 border-green-400 text-white font-bold py-2 px-4 h-12">START</button></div>
            </div>
        </section>
        <section>
            <div class="p-2">
                <a class="ml-24 italic text-xl">{{ countDownMessage }}</a>
            </div>
        </section>
        <section>
            <a class="inline-block ml-36 text-9xl">{{ timer }}</a>
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
        data() {
            return {
                countDownMessage: "More than halfway there!",
                timer: "00",
            };
        },
    };
</script>
