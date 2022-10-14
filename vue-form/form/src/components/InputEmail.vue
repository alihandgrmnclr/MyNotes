<script setup>
import { computed } from 'vue';

const props = defineProps(['email', 'label']);
const emit = defineEmits(['update:email']);

const emailHandler = event => {
    emit('update:email', event.target.value);
};

const isValidEmail = computed(() => {
    return /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(props.email);
});



</script>

<template>
    <div class="form__wrapper">
        <label class="form__label" for="email">{{label}}</label>
        <input class="form__input" type="text" name="email" id="email" :value="email"
            placeholder="Buraya mail adresinizi yazınız" @input="emailHandler">
            <template  v-if="!isValidEmail">
                <span class="form-error">Geçerli bir mail giriniz</span>
            </template>
    </div>


</template>

<style scoped>
.form__wrapper {
display: flex;
flex-direction: column;
justify-content: flex-start;
    
}


.form-error {
    font-size: 12px;
    color: red;
}
</style>
