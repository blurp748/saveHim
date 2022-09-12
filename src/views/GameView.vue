<template>
    <div class="absolute top-0 right-0 m-10"> Error(s) : {{ errorRef }}</div>

    <div class="grid content-center w-screen h-screen">
        <div class="flex justify-center m-5 mt-10">
            <div class="m-5" v-for="lesson in findLettersRef">{{lesson}}</div>
        </div>
        <div class="mt-10">
            <div class="flex justify-center gap-4 my-3 w-full">
                <kbd @click="verifyLetter('q',16)" class="kbd">{{alphabetRef[16]}}</kbd>
                <kbd @click="verifyLetter('w',22)" class="kbd">{{alphabetRef[22]}}</kbd>
                <kbd @click="verifyLetter('e',4)" class="kbd">{{alphabetRef[4]}}</kbd>
                <kbd @click="verifyLetter('r',17)" class="kbd">{{alphabetRef[17]}}</kbd>
                <kbd @click="verifyLetter('t',19)" class="kbd">{{alphabetRef[19]}}</kbd>
                <kbd @click="verifyLetter('y',24)" class="kbd">{{alphabetRef[24]}}</kbd>
                <kbd @click="verifyLetter('u',20)" class="kbd">{{alphabetRef[20]}}</kbd>
                <kbd @click="verifyLetter('i',8)" class="kbd">{{alphabetRef[8]}}</kbd>
                <kbd @click="verifyLetter('o',14)" class="kbd">{{alphabetRef[14]}}</kbd>
                <kbd @click="verifyLetter('p',15)" class="kbd">{{alphabetRef[15]}}</kbd>
            </div> 
            <div class="flex justify-center gap-4 my-3 w-full">
                <kbd @click="verifyLetter('a',0)" class="kbd">{{alphabetRef[0]}}</kbd>
                <kbd @click="verifyLetter('s',18)" class="kbd">{{alphabetRef[18]}}</kbd>
                <kbd @click="verifyLetter('d',3)" class="kbd">{{alphabetRef[3]}}</kbd>
                <kbd @click="verifyLetter('f',5)" class="kbd">{{alphabetRef[5]}}</kbd>
                <kbd @click="verifyLetter('g',6)" class="kbd">{{alphabetRef[6]}}</kbd>
                <kbd @click="verifyLetter('h',7)" class="kbd">{{alphabetRef[7]}}</kbd>
                <kbd @click="verifyLetter('j',9)" class="kbd">{{alphabetRef[9]}}</kbd>
                <kbd @click="verifyLetter('k',10)" class="kbd">{{alphabetRef[10]}}</kbd>
                <kbd @click="verifyLetter('l',11)" class="kbd">{{alphabetRef[11]}}</kbd>
            </div> 
            <div class="flex justify-center gap-4 my-3 w-full">
                <kbd @click="verifyLetter('z',25)" class="kbd">{{alphabetRef[25]}}</kbd>
                <kbd @click="verifyLetter('x',23)" class="kbd">{{alphabetRef[23]}}</kbd>
                <kbd @click="verifyLetter('c',2)" class="kbd">{{alphabetRef[2]}}</kbd>
                <kbd @click="verifyLetter('v',21)" class="kbd">{{alphabetRef[21]}}</kbd>
                <kbd @click="verifyLetter('b',1)" class="kbd">{{alphabetRef[1]}}</kbd>
                <kbd @click="verifyLetter('n',13)" class="kbd">{{alphabetRef[13]}}</kbd>
                <kbd @click="verifyLetter('m',12)" class="kbd">{{alphabetRef[12]}}</kbd>
            </div>
        </div>
        <div class="flex items-center justify-center gap-10 mt-10">
            <button @click="menu()" class="btn btn-primary btn-xs sm:btn-sm md:btn-md lg:btn-lg">Menu</button>
            <button @click="retry()" class="btn btn-primary btn-xs sm:btn-sm md:btn-md lg:btn-lg">Retry</button>
        </div>
    </div>


</template>

<script setup lang="ts">
import { ref } from 'vue';
import randomWords from 'random-words';
import { useRouter } from 'vue-router';

const router = useRouter();

let wordGeneration = randomWords(1);
let word = wordGeneration[0];
let alphabetRef = ref(['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']);
let answerLetters: string[] = [];
let findLettersRef = ref<Array<string>>([]);
let errorRef = ref(0);

for (let index = 0; index < word.length; index++) {
    answerLetters.push(word[index]);
    findLettersRef.value.push("_");
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
        }
        alphabetRef.value[pos] = ' ';
    }
}

function retry(){
    router.go(0);
}

function menu(){
    router.push("/");
}


</script> 