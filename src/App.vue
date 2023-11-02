<template>
  <div>
    <div class="head">
    <h1 class="name">금융계산기</h1>

    <!-- 버튼 -->
    <button @click="changeToDeposit" :class="depositClass">예금 계산</button>&nbsp;
    <button @click="changeToSaving" :class="savingClass">적금 계산</button>&nbsp;
    <button @click="changeToLoan" :class="loanClass">대출 계산</button>
   </div>

    <!-- 금액 입력 테이블 -->
    <depositTable v-if="currentTab == 'depositTable'" />
    <savingTable v-if="currentTab == 'savingTable'" />
    <loanTable v-if="currentTab == 'loanTable'" />
    </div>
</template>

<script setup>
  import { ref } from 'vue'

  import depositTable from './table/depositTable.vue';
  import loanTable from './table/loanTable.vue';
  import savingTable from './table/savingTable.vue';

  const depositClass = ref("btn btn-outline-primary");
  const savingClass = ref("btn btn-outline-primary");
  const loanClass = ref("btn btn-outline-primary");

  //현재 탭(지금 출력중인 테이블)
  const currentTab = ref("depositTable");

  //현재 탭 변경 메소드
  const changeToDeposit = function(){
  currentTab.value = "depositTable";
  depositClass.value = "btn btn-primary"
  savingClass.value = "btn btn-outline-primary"
  loanClass.value = "btn btn-outline-primary"
  }
  const changeToSaving = function(){
  currentTab.value = "savingTable";
  depositClass.value = "btn btn-outline-primary"
  savingClass.value = "btn btn-primary"
  loanClass.value = "btn btn-outline-primary"
  }
  const changeToLoan = function(){
  currentTab.value = "loanTable";
  depositClass.value = "btn btn-outline-primary"
  savingClass.value = "btn btn-outline-primary"
  loanClass.value = "btn btn-primary"
  }
</script>

<style scoped>

</style>