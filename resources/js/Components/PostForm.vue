<script setup>
import { ref } from 'vue';
import axios from 'axios';

const emit = defineEmits(['post-created']);

const title = ref('');
const content = ref('');
const error = ref('');
const success = ref('');

const resetForm = () => {
  title.value = '';
  content.value = '';
};

const submit = async () => {
  error.value = '';
  success.value = '';

  try {
    await axios.post('api/posts', {
      title: title.value,
      content: content.value
    });
    success.value = 'Post criado com sucesso!';
    resetForm();
    emit('post-created'); // avisa o componente pai para atualizar a lista
  } catch (err) {
    console.error('Erro ao criar post:', err);
    error.value = 'Erro ao criar post. Tente novamente.';
  }
};
</script>

<template>
  <div class="mb-6">
    <h3 class="text-lg font-semibold mb-4">Criar Post</h3>
    <div v-if="error" class="text-red-500">{{ error }}</div>
    <div v-if="success" class="text-green-500">{{ success }}</div>

    <form @submit.prevent="submit" class="space-y-4">
      <div>
        <label class="block text-sm font-medium text-gray-700">Título</label>
        <input v-model="title" type="text" class="mt-1 block w-full rounded border-gray-300" />
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700">Conteúdo</label>
        <textarea v-model="content" class="mt-1 block w-full rounded border-gray-300"></textarea>
      </div>
      <button type="submit" class="px-4 py-2 bg-blue-600 text-white rounded">Criar</button>
    </form>
  </div>
</template>
