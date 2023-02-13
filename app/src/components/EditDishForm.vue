<script setup lang="ts">
import { onMounted, ref } from "vue"
import { useDishesStore } from "@/stores/DishesStore"

const props = defineProps<{
    dishId: string
}>()

const emit = defineEmits<{
    (e: "cancel-edit-dish"): void
}>()

const dishStore = useDishesStore()

const elNameInput = ref<HTMLInputElement | null>(null)

const newDish = dishStore.getDishById(props.dishId)

const updateDish = (e: InputEvent) => {
    newDish.name = (e.target as HTMLInputElement).value
}

const cancelEdit = () => {
    emit("cancel-edit-dish")
}

onMounted(() => {
    elNameInput.value?.focus()
})
</script>

<template>
    <form @submit.prevent>
        <div class="field">
            <div class="field">
                <label for="name" class="label">Edit Name</label>
                <div class="control">
                    <input
                        :value="newDish.name"
                        @input="updateDish"
                        type="text"
                        class="input is-large"
                        placeholder="Mystery Flavored Shrimp"
                        required
                        ref="elNameInput"
                    />
                </div>
            </div>
            <div class="field">
                <div class="buttons">
                    <button @click="cancelEdit" class="button is-success">Create</button>
                    <button @click="cancelEdit" class="button is-light">Cancel</button>
                </div>
            </div>
        </div>
    </form>
</template>

<style></style>
