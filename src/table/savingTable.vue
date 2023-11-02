<template>
    <div>
        <div class="form-desc">매월 일정액을 예금하여 원하는 기간동안 모을 수 있는 금액을 계산하여 드립니다.</div>
        <table>
            <tr>
                <td class="firstCol">월납입금액</td>
                <td class="secondCol"><input type="number" @keyup="changeMonthDeposit">원</td>
            </tr>
            <tr>
                <td>목표기간</td>
                <td><input type="number" @keyup="changeGoal">개월</td>
            </tr>
            <tr>
                <td>적금금리</td>
                <td><input type="number" @keyup="changeSavingInterest">%</td>
            </tr>
        </table>
        <button class="calcButton btn btn-outline-primary" @click="savingCalc()">계산하기</button>
        <div v-if="isCalc">
        <h5>계산결과</h5>
        <ul>
            <li>원금 {{resultMonthDeposit}}원을 {{resultGoal}}개월 동안 {{resultSavingInterest}}%의 금리로 적금 시 원금 
                {{resultMonthDeposit * resultGoal}}원, 이자 {{(1+resultGoal*1) * resultMonthDeposit * resultGoal * resultSavingInterest / 2400}}원으로
                 세금우대(9.50%)가입시 {{(resultMonthDeposit * resultGoal) + (1+resultGoal*1) * 0.905 * resultMonthDeposit * resultGoal * resultSavingInterest / 2400}}을 수령하시게 됩니다.</li>
            <li>일반세율(15.40%)가입시 {{(resultMonthDeposit * resultGoal) + (1+resultGoal*1) * 0.846 * resultMonthDeposit * resultGoal * resultSavingInterest / 2400}}을 수령하시게 됩니다.</li>
        </ul>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue'; 
    const monthDeposit = ref();
    const goal = ref();
    const savingInterest = ref();
    const isCalc = ref(false);
    const resultMonthDeposit = ref();
    const resultGoal = ref();
    const resultSavingInterest = ref();
    const savingCalc = function(){
        isCalc.value = true;
        resultMonthDeposit.value = monthDeposit.value;
        resultGoal.value = goal.value;
        resultSavingInterest.value = savingInterest.value;
    }
    const changeMonthDeposit = function(event){
        monthDeposit.value = event.target.value
    }
    const changeGoal = function(event){
        goal.value = event.target.value
    }
    const changeSavingInterest = function(event){
        savingInterest.value = event.target.value
    }
</script>

<style scoped>

</style>