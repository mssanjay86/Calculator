<template>
    <div class="container">
        <div class="cal-body">

            <h1 class="margin-spacing">Calculator</h1>
            <input :value="showAnswer ? answer : substringnum" class="margin-spacing"
                style="width: 79%;margin:2% 8%;padding:10px 8px;border:none;" type="number">
            <div class="buttons">
                <div class="button margin-spacing">
                    <button :value=buttons.addSign @click="getSign($event)" class="button-styles symbols-btn">{{
                        buttons.addSign }}</button>
                </div>
                <div class="button">
                    <button :value=buttons.minusSign @click="getSign($event)" class="button-styles symbols-btn">{{
                        buttons.minusSign }}</button>
                </div>
                <div class="button">
                    <button :value=buttons.multiplySign @click="getSign($event)" class="button-styles symbols-btn">{{
                        buttons.multiplySign
                    }}</button>
                </div>
                <div class="button">
                    <button :value=buttons.divideSign @click="getSign($event)" class="button-styles symbols-btn">{{
                        buttons.divideSign }}</button>
                </div>
                <div class="numbers">
                    <div class="number-btn" v-for="num, index in calval" :key="index">
                        <div class="button" v-for="n, index1 in num" :key="index1">
                            <button class="button-styles" @click="getNumber(n)">{{ n }}</button>
                        </div>

                    </div>

                    <div class="button">
                        <button @click="calculate" style="position: relative; left: 325px; bottom: 257px; height: 157px;"
                            class="button-styles symbols-btn">=</button>


                    </div>

                </div>

            </div>

        </div>
    </div>
</template>
<script lang="ts" setup>
import { ref } from "vue";

const calval = [["7", "8", "9"], ["4", "5", "6"], ["1", "2", "3"], ["0", "Clear"]]

const buttons = ref(
    {

        addSign: '+',
        minusSign: '-',
        multiplySign: '*',
        divideSign: '/'
    }
)

const count = ref(0);

const substringnum = ref('0');
const answer = ref(0)
const sign = ref('')
const isPushed = ref(false)

const getNumber = (num: string) => {
    showAnswer.value = false;
    if (substringnum.value == '0') {
        substringnum.value = '';
    }
    if (num == "Clear") {
        substringnum.value = "0"
    }
    substringnum.value = substringnum.value + num;



}
const showAnswer = ref(false);
const getSign = (e: any) => {
    sign.value = e.target.value;
    answer.value = answer.value + parseInt(substringnum.value)
    substringnum.value = '';
    isPushed.value = true;
}

const clearValue = () => {
    showAnswer.value = false;
}


const calculate = () => {

    if (sign.value == '+') {
        answer.value = answer.value + parseInt(substringnum.value);
        substringnum.value = '';
        showAnswer.value = true;

    } else if (sign.value == '-') {
        answer.value = answer.value - parseInt(substringnum.value);
        substringnum.value = '';
        showAnswer.value = true;
    }
    else if (sign.value == '*') {
        answer.value = answer.value * parseInt(substringnum.value);
        substringnum.value = '';
        showAnswer.value = true;
    }
    else if (sign.value == '/') {
        answer.value = answer.value / parseInt(substringnum.value);
        substringnum.value = '';
        showAnswer.value = true;
    }

}

</script>
