<template>
    <div>
        <div class="form-desc">목돈을 일정기간 예치 했을 때 만기 지급액을 계산하여 드립니다.</div>
            <table>
                <tr>
                    <td class="firstCol">예치금액</td>
                    <td class="secondCol"><input @keydown.enter="depositCalc()"  @keyup="changeDepositCost" type="number">원</td>
                </tr>
                <tr>
                    <td>예치기간</td>
                    <td><input @keydown.enter="depositCalc()" @keyup="changeDepositPeriod" type="number">개월</td>
                </tr>
                <tr>
                    <td>이자구분</td>
                    <td><select class="form-select" v-model="method">
                        <option value="single">단리</option>
                        <option value="compound">복리</option>
                    </select></td>
                </tr>
                <tr>
                    <td>이자율</td>
                    <td><input @keydown.enter="depositCalc()" @keyup="changeDepositInterest" type="number">%</td>
                </tr>
            </table>
            <button class="calcButton btn btn-outline-primary" @click="depositCalc()">계산하기</button>
            <div v-if="isCalc">
            <h5>계산결과</h5>
            <ul>
                <li>일반세율(15.40%)가입시 {{Math.floor(result)}}원을 수령하시게 됩니다.</li>
            </ul>
            </div>
            <div v-if="isError">
            <h5>오류</h5>
            <ul>
                <li>적절한 값을 입력해주세요.</li>
            </ul>
            </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue'; 
    const depositCost = ref(0);
    const method = ref('single');
    const depositPeriod = ref(0);
    const depositInterest = ref(0);
    const isCalc = ref(false);
    const isError = ref(false);
    const result = ref(0);
    const depositCalc = function() {
        if(depositCost.value*1==NaN || depositCost.value*1<0 || Number.isInteger(depositCost.value*1)==false 
        || depositPeriod.value*1==NaN || depositPeriod.value*1<0 || Number.isInteger(depositPeriod.value*1)==false
        || depositInterest.value*1 ==NaN || depositInterest.value*1<0){
            isError.value = true;
            isCalc.value = false;
        }
        else if(method.value=='single'){
            result.value = depositCost.value*1 +
            (depositCost.value * depositPeriod.value * depositInterest.value / 1200 * 0.846);
            console.log(depositCost.value * depositPeriod.value);
            isCalc.value = true;
            isError.value = false;
        }
        else{
            result.value = depositCost.value*1 +
            (depositCost.value*((1+(depositInterest.value/1200))**depositPeriod.value)-depositCost.value)*0.846;
            isCalc.value = true;
            isError.value = false;
        }
        
    }


    const changeDepositCost = function(event){
        depositCost.value = event.target.value
    }
    const changeDepositPeriod = function(event){
        depositPeriod.value = event.target.value
    }
    const changeDepositInterest = function(event){
        depositInterest.value = event.target.value
    }
</script>

<style scoped>

</style>