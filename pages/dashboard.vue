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

    <Modal ref="modal" v-model:isOpen="isOpen" class="text-lg">
      <p><strong>Nome:</strong> {{ selectedClient.name }}</p>
      <p><strong>CEP:</strong> {{ selectedClient.cep }}</p>
      <p><strong>Estado:</strong> {{ selectedClient.estado }}</p>
      <p><strong>Cidade:</strong> {{ selectedClient.cidade }}</p>
      <p><strong>Bairro:</strong> {{ selectedClient.bairro }}</p>
      <p><strong>Logradouro:</strong> {{ selectedClient.logradouro }}</p>
      <p><strong>Número:</strong> {{ selectedClient.numero }}</p>
    </Modal>

    <Modal ref="modal" v-model:isOpen="isOpen1" class="text-lg">
      Adicionar novo
    </Modal>
  </div>
</template>
