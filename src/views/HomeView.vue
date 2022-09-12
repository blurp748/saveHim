<template>
    <div class="hero min-h-screen bg-base-200">
        <div class="hero-content text-center">
                <div class="max-w-md">
                    <h1 class="text-5xl font-bold m-10">Save Him !</h1>
                    <button @click="game()" class="btn btn-primary">
                        Let's go
                    </button>
                </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';

const router = useRouter();

function game(){
    router.push("/game");
}

</script>