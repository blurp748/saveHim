<template>
    <div class="absolute top-0 right-0 m-10"> Error(s) : {{ errorRef }}</div>

    <input v-model="showModal" type="checkbox" id="my-modal-4" class="modal-toggle" />
    <label for="my-modal-4" class="modal cursor-pointer">
    <label class="modal-box relative" for="">
        <h3 v-if="errorRef < errorAllowedRef" class="text-lg font-bold">You win !</h3>
        <h3 v-else class="text-lg font-bold">You lose ..</h3>
        <p v-if="errorRef < errorAllowedRef" class="py-4">You've made {{ errorRef }} error(s)</p>
        <p v-else class="py-4">The word was {{ wordRef }}.</p>
    </label>
    </label>

    <div class="grid content-center w-screen h-screen">
        <div class="flex justify-center m-5 mt-10">
            <div class="m-5" v-for="lesson in findLettersRef">{{lesson}}</div>
        </div>
        <div class="mt-10">
            <div class="flex justify-center gap-2 my-3 w-full">
                <kbd @click="verifyLetter('q',16)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[16]}}</kbd>
                <kbd @click="verifyLetter('w',22)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[22]}}</kbd>
                <kbd @click="verifyLetter('e',4)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[4]}}</kbd>
                <kbd @click="verifyLetter('r',17)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[17]}}</kbd>
                <kbd @click="verifyLetter('t',19)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[19]}}</kbd>
                <kbd @click="verifyLetter('y',24)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[24]}}</kbd>
                <kbd @click="verifyLetter('u',20)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[20]}}</kbd>
                <kbd @click="verifyLetter('i',8)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[8]}}</kbd>
                <kbd @click="verifyLetter('o',14)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[14]}}</kbd>
                <kbd @click="verifyLetter('p',15)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[15]}}</kbd>
            </div> 
            <div class="flex justify-center gap-2 my-3 w-full">
                <kbd @click="verifyLetter('a',0)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[0]}}</kbd>
                <kbd @click="verifyLetter('s',18)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[18]}}</kbd>
                <kbd @click="verifyLetter('d',3)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[3]}}</kbd>
                <kbd @click="verifyLetter('f',5)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[5]}}</kbd>
                <kbd @click="verifyLetter('g',6)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[6]}}</kbd>
                <kbd @click="verifyLetter('h',7)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[7]}}</kbd>
                <kbd @click="verifyLetter('j',9)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[9]}}</kbd>
                <kbd @click="verifyLetter('k',10)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[10]}}</kbd>
                <kbd @click="verifyLetter('l',11)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[11]}}</kbd>
            </div> 
            <div class="flex justify-center gap-2 my-3 w-full">
                <kbd @click="verifyLetter('z',25)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[25]}}</kbd>
                <kbd @click="verifyLetter('x',23)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[23]}}</kbd>
                <kbd @click="verifyLetter('c',2)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[2]}}</kbd>
                <kbd @click="verifyLetter('v',21)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[21]}}</kbd>
                <kbd @click="verifyLetter('b',1)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[1]}}</kbd>
                <kbd @click="verifyLetter('n',13)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[13]}}</kbd>
                <kbd @click="verifyLetter('m',12)" class="kbd kbd-sm md:kbd-md lg:kbd-lg">{{alphabetRef[12]}}</kbd>
            </div>
        </div>
        <div class="flex items-center justify-center gap-10 mt-10">
            <button @click="menu()" class="btn btn-primary btn-xs sm:btn-sm md:btn-md lg:btn-lg">Menu</button>
            <button @click="launchGame()" class="btn btn-primary btn-xs sm:btn-sm md:btn-md lg:btn-lg">Retry</button>
        </div>
    </div>


</template>

<script setup lang="ts">

// ----------------------------------------
// 					Imports
// ----------------------------------------

import { ref } from 'vue';
import randomWords from 'random-words';
import { useRouter, useRoute } from 'vue-router';

// ----------------------------------------
// 				Data variables
// ----------------------------------------

const router = useRouter();
const route = useRoute();

let alphabetRef = ref(['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']);
let answerLetters: string[] = [];
let findLettersRef = ref<Array<string>>([]);
let showModal = ref(false);
let errorRef = ref(0);
let errorAllowedRef = ref(0);
let wordRef = ref("");

// ----------------------------------------
// 					Logic
// ----------------------------------------

launchGame();

// ----------------------------------------
// 				  Functions
// ----------------------------------------

function launchGame(){

    const difficulty = route.params.difficulty;
    let minLength = 4;
    let wordGeneration = randomWords(1);

    alphabetRef.value = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'];
    answerLetters = [];
    findLettersRef.value = [];
    showModal.value = false;
    errorRef.value = 0;
    errorAllowedRef.value = 15;

    switch(difficulty){
        case 'medium':
            errorAllowedRef.value = 10;
            minLength = 6;
            break;
        case 'hard':
            errorAllowedRef.value = 5;
            minLength = 8;
            break;
        default:
            break;
    }

    while(wordGeneration[0].length < minLength){
        wordGeneration = randomWords(1);
    }

    wordRef.value = wordGeneration[0];

    for (let index = 0; index < wordRef.value.length; index++) {
        answerLetters.push(wordRef.value[index]);
        findLettersRef.value.push("_");
    }

    // Number of clues
    minLength = 3;

    switch(difficulty){
        case 'medium':
            minLength = 2;
            break;
        case 'hard':
            minLength = 1;
            break;
        default:
            break;
    }

    // Setting up clues
    for (let index = 0; index < minLength; index++) {

        let random = getRandomInt(wordRef.value.length);

        while(findLettersRef.value[random] != '_'){
            random = getRandomInt(wordRef.value.length);
        }

        let clueLetter = wordRef.value.charAt(random);

        for (let index2 = 0; index2 < wordRef.value.length; index2++) {
            if(wordRef.value[index2] == clueLetter){
                findLettersRef.value[index2] = wordRef.value[index2];
            }
        }

        for(let index2 in alphabetRef.value){
            if(alphabetRef.value[index2] == clueLetter){
                alphabetRef.value[index2] = ' ';
                break;
            }
        }
    }

    // Verify is clues doesn't give the complete word
    if(isCompleted()) launchGame();
}

function verifyLetter(letter: string, pos: number) {
    if(alphabetRef.value[pos] != ' '){
        if(answerLetters.some(elt => elt == letter)){
            for(let elt in answerLetters){
                if(answerLetters[elt] == letter){
                    findLettersRef.value[elt] = letter;
                }
            }
        }else{
            errorRef.value++;
            if(errorRef.value > errorAllowedRef.value) showModal.value = true;
        }
        alphabetRef.value[pos] = ' ';
        if(isCompleted()) showModal.value = true;
    }
}

function isCompleted(){
    for(const ind in findLettersRef.value){
        if(findLettersRef.value[ind] == '_'){
            return false;
        }
    }
    return true;

}

function menu(){
    router.push("/");
}

function getRandomInt(max: number) {
  return Math.floor(Math.random() * max);
}


</script> 