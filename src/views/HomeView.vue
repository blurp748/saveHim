<template>
    <div class="hero min-h-screen bg-base-200">
        <div class="hero-content text-center">
                <div class="max-w-md -mt-40">
                    <h1 class="text-5xl font-bold m-10">Save Him !</h1>
                    <button @click="game('easy')" class="btn btn-primary mr-3">
                        Easy
                    </button>
                    <button @click="game('medium')" class="btn btn-primary">
                        Medium
                    </button>
                    <button @click="game('hard')" class="btn btn-primary ml-3">
                        Hard
                    </button>
                </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';

const router = useRouter();

function game(difficulty: string){
    router.push('/game/' + difficulty);
}

</script>