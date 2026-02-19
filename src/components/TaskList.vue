<script setup lang="ts">
import type { Task } from "@/types";

const props = defineProps<{
	tasks: Task[];
}>();

const emits = defineEmits<{
	toggleDone: [id: string];
	removeTask: [id: string];
}>();
</script>

<template>
	<TransitionGroup name="task" tag="div" class="task-list">
		<article v-for="task in props.tasks" :key="task.id" class="task">
			<label>
				<input
					@input="emits('toggleDone', task.id)"
					type="checkbox"
					:checked="task.done" />
				<span :class="{ done: task.done }">{{ task.title }}</span>
			</label>
			<button class="outline" @click="emits('removeTask', task.id)">
				Remove
			</button>
		</article>
	</TransitionGroup>
</template>

<style>
.task-list {
	margin-top: 1rem;
}
.done {
	text-decoration: line-through;
}
.task {
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.task-enter-active,
.task-leave-active {
  transition: all 0.5s ease;
}
.task-enter-from,
.task-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
