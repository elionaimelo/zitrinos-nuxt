<script lang="ts" setup>
definePageMeta({
  title: "Login",
});

const { auth } = useSupabaseClient();
const user = useSupabaseUser();

const data = reactive({
  email: "",
  password: "",
});

const isLoading = ref(false);
const errormsg = ref(false);

const onSignIn = async () => {
  isLoading.value = true;
  const { error } = await auth.signInWithPassword({
    email: data.email,
    password: data.password,
  });

  if (error) {
    errormsg.value = true;
    isLoading.value = false;
    return;
  }

  isLoading.value = false;
  navigateTo("/dashboard");
};
if (user.value) {
  navigateTo("/dashboard");
}
</script>

<template>
  <!-- component -->
  <div>
    <div
      class="toast toast-top toast-center absolute z-50 w-1/5 px-5"
      v-if="errormsg"
    >
      <div class="alert bg-red-500 text-white text-center">
        <p class="block w-full">Erro ao fazer login</p>
      </div>
    </div>
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
        <div
          class="flex-col flex self-center p-10 sm:max-w-5xl xl:max-w-2xl z-10"
        >
          <div class="self-start hidden lg:flex flex-col text-white">
            <img src="" class="mb-3" />
            <h1 class="mb-3 font-bold text-5xl">Olá, Seja bem vindo</h1>
            <p class="pr-3">
              Lorem ipsum is placeholder text commonly used in the graphic,
              print, and publishing industries for previewing layouts and visual
              mockups
            </p>
          </div>
        </div>
        <div class="flex justify-center self-center z-10">
          <div class="p-12 bg-white mx-auto rounded-2xl w-100">
            <div
              v-if="isLoading"
              class="home-loading flex justify-center items-center"
            >
              Carregando...
            </div>
            <div v-else>
              <div class="mb-4">
                <h3 class="font-semibold text-2xl text-gray-800">Login</h3>
                <p class="text-gray-500">Insira seus dados abaixo.</p>
              </div>
              <div class="space-y-5">
                <div class="space-y-2">
                  <label class="text-sm font-medium text-gray-700 tracking-wide"
                    >Email</label
                  >
                  <input
                    class="w-full text-base px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-400"
                    type="email"
                    placeholder="zitrino@gmail.com"
                    v-model="data.email"
                    required
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
                    required
                  />
                </div>
                <div class="flex items-center justify-between">
                  <div class="text-sm">
                    <a href="#" class="text-indigo-400 hover:text-indigo-500">
                      Esqueceu sua senha?
                    </a>
                  </div>
                </div>
                <div>
                  <button
                    class="btn btn-primary w-full rounded-full"
                    @click="onSignIn"
                  >
                    Entrar
                  </button>
                  <a
                    href="cadastro"
                    class="btn btn-secondary w-full rounded-full mt-2"
                  >
                    Cadastrar
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
