<template>
  <div class="w-full mx-[20px] flex flex-col items-center space-y-3">
    <h2 class="text-center text-[40px] font-bold text-white">Add questions</h2>
    <form @submit.prevent="addQuestion" class="w-full">
      <textarea
        v-model="newQuestion"
        placeholder="Enter your question"
        class="w-full rounded-[10px]"
      />
      <option-form-component
        v-for="(option, index) in options"
        :key="index"
        :option="option"
      />
      <div class="flex flex-col space-y-3">
        <button
          type="button"
          @click="addOption"
          class="bg-[#0d2137] text-[#fff] p-[10px] rounded-[10px] w-[30%]"
        >
          Add Option
        </button>
        <button
          type="submit"
          class="bg-[#0d2137] text-[#fff] p-[10px] rounded-[10px] w-[30%]"
        >
          Add Question
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import OptionFormComponent from "./OptionFormComponent.vue";
import { ref } from "vue";

export default {
  setup(_, { emit }) {
    const newQuestion = ref("");
    const options = ref([]);

    function addOption() {
      options.value.push({ value: "", correct: false });
    }

    function addQuestion() {
      emit('add-question', { question: newQuestion.value, options: options.value });
      newQuestion.value = '';
      options.value = [];
    }

    return {
      newQuestion,
      options,
      addOption,
      addQuestion,
    };
  },
  components: {
    OptionFormComponent,
  },
};
</script>