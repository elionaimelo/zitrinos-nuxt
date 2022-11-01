<script lang="ts" setup>
definePageMeta({
  title: "Cadastro",
});

const client = useSupabaseClient();
const user = useSupabaseUser();

const data = reactive({
  name: "",
  email: "",
  password: "",
});

const isLoading = ref(false);

const onSubmit = async () => {
  isLoading.value = true;
  const { error } = await client.auth.signUp(
    {
      email: data.email,
      password: data.password,
    },
    {
      data: {
        name: data.name,
      },
    }
  );

  if (error) {
    isLoading.value = false;
    console.log(error.message);
    return;
  } else {
    isLoading.value = false;
    navigateTo("/");
  }
};
</script>

<template>
  <!-- component -->
  <div
    class="bg-no-repeat bg-cover bg-center relative"
    style="
      background-image: url(https://images.unsplash.com/photo-1579621970563-ebec7560ff3e?ixlib=rb-1.2.1&amp;ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&amp;auto=format&amp;fit=crop&amp;w=1951&amp;q=80);
    "
  >
    <div
      class="absolute bg-gradient-to-b from-indigo-500 to-indigo-400 opacity-75 inset-0 z-0"
    ></div>
    <div class="min-h-screen sm:flex sm:flex-row mx-0 justify-center">
      <div class="flex justify-center self-center z-10">
        <div class="p-12 bg-white mx-auto rounded-2xl w-100">
          <div class="mb-4">
            <h3 class="font-semibold text-2xl text-gray-800">Cadastro</h3>
            <p class="text-gray-500">
              Insira seus dados abaixo para realizar seu cadastro.
            </p>
          </div>
          <div class="space-y-5">
            <div class="space-y-2">
              <label class="text-sm font-medium text-gray-700 tracking-wide"
                >Nome</label
              >
              <input
                class="w-full text-base px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-400"
                type="text"
                placeholder="Insira seu nome"
                v-model="data.name"
              />
            </div>
            <div class="space-y-2">
              <label class="text-sm font-medium text-gray-700 tracking-wide"
                >Email</label
              >
              <input
                class="w-full text-base px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-400"
                type="email"
                placeholder="mail@gmail.com"
                v-model="data.email"
              />
            </div>
            <div class="space-y-2">
              <label
                class="mb-5 text-sm font-medium text-gray-700 tracking-wide"
              >
                Senha
              </label>
              <input
                class="w-full content-center text-base px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-400"
                type="password"
                placeholder="Insira sua senha"
                v-model="data.password"
              />
            </div>
            <div class="md:flex">
              <a href="/" class="btn btn-secondary w-2/4 rounded-full mr-3">
                Voltar
              </a>
              <button
                class="btn btn-primary w-2/4 rounded-full"
                @click="onSubmit"
                :disabled="isLoading"
              >
                <nuxt-icon
                  name="iconphone"
                  fill
                  class="icon"
                  v-if="isLoading"
                />Cadastrar
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
