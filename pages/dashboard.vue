<script lang="ts" setup>
import Modal from "../components/Modal.vue";

definePageMeta({
  middleware: ["auth"],
  layout: "dashboard",
  title: "Dashboard",
});

const selectedClient = ref({});
const isOpen = ref(false);
const isOpen1 = ref(false);
const client = useSupabaseClient();
const modal = ref();
const form = reactive({
  nome: "",
  cep: "",
  estado: "",
  cidade: "",
  bairro: "",
  logradouro: "",
  numero: "",
  cpf: "",
  complemento: "",
});

const { data: clients } = await useAsyncData("clients", async () => {
  const { data, error } = await client.from("clients").select("*");

  if (error) {
    console.log(error);
    return;
  }

  return data;
});

const onDetail = (id: string) => {
  const client = clients.value.find((client) => client.id === id);
  selectedClient.value = client;
  isOpen.value = true;
};

const showModal = () => {
  isOpen1.value = true;
};

const onSearchAddress = async (event) => {
  if (event.target.value.length === 8) {
    const { data } = await useFetch(
      `https://opencep.com/v1/${event.target.value}.json`
    );

    form.estado = data.value.uf;
    form.cidade = data.value.localidade;
    form.bairro = data.value.bairro;
    form.logradouro = data.value.logradouro;
  }
};

const addClient = async () => {
  const { error } = await client.from("clients").insert([
    {
      name: form.nome,
      cep: form.cep,
      estado: form.estado,
      cidade: form.cidade,
      bairro: form.bairro,
      logradouro: form.logradouro,
      numero: form.numero,
      cpf: form.cpf,
      complemento: form.complemento,
    },
  ]);

  if (error) {
    console.log(error);
    return;
  }

  isOpen1.value = false;
  location.reload();
};
</script>

<template>
  <div>
    <div class="overflow-x-auto w-full">
      <h3 class="text-3xl mb-9 font-semibold text-indigo-700">Dashboard</h3>
      <div class="flex justify-between">
        <h3 class="text-2xl">Lista de clientes</h3>
        <button class="btn btn-primary mb-4" @click="showModal">
          Adicionar novo
        </button>
      </div>
      <table class="table w-full">
        <!-- head -->
        <thead>
          <tr>
            <td>
              <label>
                <input type="checkbox" class="checkbox" />
              </label>
            </td>
            <th>Nome</th>
            <th>Endereço</th>
            <th>CPF</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <!-- row 1 -->
          <tr v-for="item in clients">
            <td>
              <label>
                <input type="checkbox" class="checkbox" />
              </label>
            </td>
            <td>
              <div class="flex items-center space-x-3">
                <div>
                  <div class="font-bold">{{ item.name }}</div>
                </div>
              </div>
            </td>
            <td>
              {{ item.logradouro }}, {{ item.numero }}
              <br />
              <span class="badge badge-ghost badge-sm"
                >{{ item.cidade }} - {{ item.estado }}</span
              >
            </td>
            <td>{{ item.cpf }}</td>
            <th>
              <button class="btn btn-ghost btn-xs" @click="onDetail(item.id)">
                Detalhes
              </button>
            </th>
          </tr>
        </tbody>
      </table>
    </div>

    <Modal ref="modal" name="md1" v-model:isOpen="isOpen" class="text-lg">
      <template #title>
        <h3 class="text-2xl font-semibold">{{ selectedClient.name }}</h3>
      </template>
      <template #body>
        <p><strong>Nome:</strong> {{ selectedClient.name }}</p>
        <p><strong>CEP:</strong> {{ selectedClient.cep }}</p>
        <p><strong>Estado:</strong> {{ selectedClient.estado }}</p>
        <p><strong>Cidade:</strong> {{ selectedClient.cidade }}</p>
        <p><strong>Bairro:</strong> {{ selectedClient.bairro }}</p>
        <p><strong>Logradouro:</strong> {{ selectedClient.logradouro }}</p>
        <p><strong>Número:</strong> {{ selectedClient.numero }}</p>
      </template>
    </Modal>

    <Modal ref="modal" name="md2" v-model:isOpen="isOpen1" class="text-lg">
      <template #title>
        <h3 class="text-2xl font-semibold">Adicionar novo cliente</h3>
      </template>
      <template #body>
        <form class="flex flex-col gap-y-2">
          <div>
            <label>Nome</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.nome"
              required
            />
          </div>
          <div>
            <label>CPF</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.cpf"
              pattern="[0-9]{3}.[0-9]{3}.[0-9]{3}-[0-9]{2}"
              required
            />
          </div>
          <div>
            <label>CEP</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.cep"
              @keyup="onSearchAddress"
            />
          </div>
          <div>
            <label>Estado</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.estado"
            />
          </div>
          <div>
            <label>Cidade</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.cidade"
            />
          </div>
          <div>
            <label>Bairro</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.bairro"
            />
          </div>
          <div>
            <label>Logradouro</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.logradouro"
            />
          </div>
          <div>
            <label>Número</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.numero"
            />
          </div>
          <div>
            <label>Complemento</label>
            <input
              type="text"
              class="input input-bordered w-full"
              v-model="form.complemento"
            />
          </div>
          <div>
            <button
              class="btn btn-primary my-4 md:float-right md:w-1/3"
              @click="addClient"
            >
              Adicionar
            </button>
          </div>
        </form>
      </template>
    </Modal>
  </div>
</template>
