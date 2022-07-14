<template>
<div>
  <AppPageHeading>
    {{ board.title }}
  </AppPageHeading>
  <BoardMenu :board="board" @deleteBoard="deleteBoardIfConfirmed" />

  <BoardDragAndDrop
    :tasks="tasks"
    :board="board"
    @update="updateBoard"
    :addTask="addTask"
  />
</div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { useRoute } from "vue-router";
import type { Task } from "@/types";
import BoardDragAndDrop from "@/components/BoardDragAndDrop.vue";
import { v4 as uuidv4 } from "uuid";

const route = useRoute();

const id = route.params.id;

const board = ref({
    id: id || "1",
    title: "some hardcoded title",
    order: JSON.stringify([
        { id: "1", title: "backlog 🌴", taskIds: ["1", "2"] },
    ]),
});

const tasks = ref<Partial<Task>[]>([
    { id: "1", title: "make toasts" },
    { id: "2", title: "clean room" },
]);

async function addTask(task: Task) {
    return new Promise((resolve, reject) => {
        const taskWithTheId = {
            ...task,
            id: uuidv4(),
        };
        tasks.value.push(taskWithTheId);
        resolve(taskWithTheId);
    });
}

const updateBoard = (b) => {
    board.value = b;
    // alerts.success("Board updated!");
};

const deleteBoardIfConfirmed = () => {
    console.log("delete board");
};

</script>

<style scoped>

</style>