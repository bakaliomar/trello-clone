<script setup lang="ts">
import { Button as KButton } from "@progress/kendo-vue-buttons";
import { Popup as KPopup } from "@progress/kendo-vue-popup";
import { ref } from "vue";

const showTeams = ref(false);
</script>

<template>
  <div class="flex p-4 border-bottom border-2 justify-between">
    <router-link to="/">
      <div class="logo uppercase font-bold text-2xl">Othello</div>
    </router-link>
    <div>
      <button
        ref="button"
        class="mr-5 text-[#ff6358]"
        @click="showTeams = !showTeams"
      >
        <span class="k-icon k-i-ungroup"></span>
        My Team
      </button>

      <KPopup :anchor="'button'" :show="showTeams" class="mt-5">
        <ul>
          <li
            class="px-5 cursor-pointer hover:bg-red-300 py-2"
            @click="showTeams = false"
          >
            Team 1
          </li>
          <li
            class="px-5 cursor-pointer hover:bg-red-300 py-2"
            @click="showTeams = false"
          >
            Team 2
          </li>
        </ul>
      </KPopup>

      <KButton
        :rounded="'full'"
        :shape="'rectangle'"
        :icon="'logout'"
        :theme-color="'warning'"
        >Logout</KButton
      >
    </div>
  </div>
</template>
