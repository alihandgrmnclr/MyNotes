<script setup>
import { computed } from 'vue';

const props = defineProps(['name', 'label']);
const emit = defineEmits(['update:name']);

const nameHandler = event => {
    emit('update:name', event.target.value);
};

const isValidName = computed(() => {
    return props.name.length > 1;
});

</script>

<template>

    <div class="form__wrapper">
        <label class="form__label" for="name">{{label}}</label>
        <input class="form__input" type="text" name="name" id="name" :value="name" placeholder="Buraya isminizi yazınız"
            @input="nameHandler">
        <template v-if="!isValidName">
            <span class="form-error">Boş Geçilemez</span>
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
