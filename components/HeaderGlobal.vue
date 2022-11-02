<script lang="ts" setup>
const { auth } = useSupabaseClient();

const signOut = async () => {
  const { error } = await auth.signOut();
  if (error) {
    return;
  } else {
    navigateTo("/");
  }
};
</script>

<template>
  <div class="navbar bg-base-100 px-0 shadow-md z-50 sticky">
    <div class="container mx-auto">
      <!-- para o mobile -->
      <!-- <div class="flex-none">
      <div class="navbar-start">
        <div class="dropdown">
          <label
            tabindex="0"
            class="btn btn-ghost btn-circle hover:bg-transparent justify-start"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h7"
              />
            </svg>
          </label>
          <ul
            tabindex="0"
            class="menu menu-compact dropdown-content mt-3 p-2 shadow bg-base-100 rounded-box w-52"
          >
            <li><a>Homepage</a></li>
            <li><a>Portfolio</a></li>
            <li><a>About</a></li>
          </ul>
        </div>
      </div>
    </div> -->
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-xl">Zitrinos</a>
      </div>
      <div class="flex-none">
        <ul class="menu menu-horizontal p-0">
          <li tabindex="0">
            <a>
              <svg width="32" height="32" viewBox="0 0 32 32">
                <path fill="#888888" d="M16 8a5 5 0 1 0 5 5a5 5 0 0 0-5-5Z" />
                <path
                  fill="currentColor"
                  d="M16 2a14 14 0 1 0 14 14A14.016 14.016 0 0 0 16 2Zm7.992 22.926A5.002 5.002 0 0 0 19 20h-6a5.002 5.002 0 0 0-4.992 4.926a12 12 0 1 1 15.985 0Z"
                />
              </svg>
              <svg
                class="fill-current"
                xmlns="http://www.w3.org/2000/svg"
                width="20"
                height="20"
                viewBox="0 0 24 24"
              >
                <path
                  d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z"
                />
              </svg>
            </a>
            <ul class="p-2 bg-base-100 shadow-sm">
              <li><a href="#" @click="signOut">Sair</a></li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
