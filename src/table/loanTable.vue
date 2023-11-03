<template>
    <div>
        <div class="form-desc">대출금액의 상환금액과 일정을 계산하여 드립니다.</div>
        <table>
            <tr>
                <td class="firstCol">상환방법</td>
                <td class="secondCol ">
                    <div>
                    <input class="align-middle" type="radio" name="select" id="expirePayment" value="expirePayment" v-model="method" ><label for="expirePayment">만기일시상환</label>
                    <input class="align-middle" type="radio" name="select" id="equalPayment" value="equalPayment" v-model="method"><label for="equalPayment">원금균등상환</label>
                    <input class="align-middle" type="radio" name="select" id="interestEqualPayment" value="interestEqualPayment" v-model="method"><label for="interestEqualPayment">원리금균등상환</label>
                    </div>
                </td>
            </tr>
            <tr>
                <td>대출금액</td>
                <td><input type="number" @keydown.enter="loanCalc()" @input="changeLoanAmount">원</td>
            </tr>
            <tr>
                <td>대출기간</td>
                <td><input type="number" @keydown.enter="loanCalc()" @input="changeLoanTerm">개월</td>
            </tr>
            <tr>
                <td>대출금리</td>
                <td><input type="number" @keydown.enter="loanCalc()" @input="changeInterestRate">%</td>
            </tr>
        </table>
        <button class="calcButton btn btn-outline-primary" @click="loanCalc()">계산하기</button>
        <div v-if="isCalc">
            <h5>계산결과</h5>
            <ul v-if="method=='expirePayment'">
                <li>원금 {{resultLoanAmount}}원을 {{resultLoanTerm}}개월 동안 {{resultInterestRate}}%의 금리로 대출 시 원금 {{resultLoanAmount}}원, 이자 
                    {{Math.floor(resultLoanAmount * resultLoanTerm * resultInterestRate / 1200)}}원을 만기 일시 상환하시게 됩니다.</li>
            </ul>
            <ul v-if="method=='equalPayment'">
                <li>원금 {{resultLoanAmount}}원을 {{resultLoanTerm}}개월 동안 {{resultInterestRate}}%의 금리로 대출 시 매 달 aa원을 원금 균등 상환하시게 됩니다.</li>
            </ul>
            <ul v-if="method=='interestEqualPayment'">
                <li>원금 {{resultLoanAmount}}원을 {{resultLoanTerm}}개월 동안 {{resultInterestRate}}%의 금리로 대출 시 매 달 aa원을 원리금 균등 상환하시게 됩니다.</li>
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
    const loanAmount = ref();
    const loanTerm = ref();
    const interestRate = ref();
    const method = ref('expirePayment');
    const isCalc = ref(false);
    const resultLoanAmount = ref();
    const resultLoanTerm = ref();
    const resultInterestRate = ref();
    const isError = ref();
    const loanCalc = function(){
        resultLoanAmount.value = loanAmount.value;
        resultLoanTerm.value = loanTerm.value;
        resultInterestRate.value = interestRate.value;
        if(resultLoanAmount.value*1==NaN || resultLoanAmount.value*1<0 || Number.isInteger(resultLoanAmount.value*1)==false 
        || resultLoanTerm.value*1==NaN || resultLoanTerm.value*1<0 || Number.isInteger(resultLoanTerm.value*1)==false
        || resultInterestRate.value*1 ==NaN || resultInterestRate.value*1<0){
            isError.value = true;
            isCalc.value = false;
        }
        else{
            isCalc.value = true;
            isError.value = false;
        }
    }
    const changeLoanAmount = function(event){
        loanAmount.value = event.target.value
    }
    const changeLoanTerm = function(event){
        loanTerm.value = event.target.value
    }
    const changeInterestRate = function(event){
        interestRate.value = event.target.value
    }
</script>

<style scoped>

</style>