<script lang="ts" setup>
definePageMeta({
  middleware: ["auth"],
  layout: "dashboard",
  title: "Dashboard",
});
</script>

<template>
  <div>
    <div class="overflow-x-auto w-full">
      <table class="table w-full">
        <!-- head -->
        <thead>
          <tr>
            <th>
              <label>
                <input type="checkbox" class="checkbox" />
              </label>
            </th>
            <th>Nome</th>
            <th>Endereço</th>
            <th>CPF</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <!-- row 1 -->
          <tr>
            <th>
              <label>
                <input type="checkbox" class="checkbox" />
              </label>
            </th>
            <td>
              <div class="flex items-center space-x-3">
                <div class="avatar">
                  <div class="mask mask-squircle w-12 h-12">
                    <img
                      src="https://randomuser.me/api/portraits/men/44.jpg"
                      alt="Avatar Tailwind CSS Component"
                    />
                  </div>
                </div>
                <div>
                  <div class="font-bold">Hart Hagerty</div>
                </div>
              </div>
            </td>
            <td>
              Av das Alagoas, 1234
              <br />
              <span class="badge badge-ghost badge-sm"
                >Natal - Rio Grande do Norte</span
              >
            </td>
            <td>123.456.789-10</td>
            <th>
              <button class="btn btn-ghost btn-xs">Detalhes</button>
            </th>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
