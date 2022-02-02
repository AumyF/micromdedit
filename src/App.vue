<script setup lang="ts">
import { computed, ref } from "vue";
import { micromark } from "micromark";
import { TabGroup, TabList, TabPanels, TabPanel, Tab } from "@headlessui/vue";
import HtmlViewer from "./components/HtmlViewer.vue";

const textarea = ref<HTMLTextAreaElement | null>(null);
const markdownContent = ref("");
const htmlContent = computed(() => micromark(markdownContent.value));

const insert = (text: string) => {
  if (textarea.value === null) return;
  const cursorPosition = textarea.value.selectionStart;
  markdownContent.value =
    markdownContent.value.substring(0, cursorPosition) +
    text +
    markdownContent.value.substring(cursorPosition);
};
</script>

<template>
  <div class="container mx-auto p-8 flex flex-col gap-4">
    <TabGroup>
      <TabList class="flex gap-2">
        <Tab>
          <button class="p-2 bg-blue-500 rounded text-white">
            Edit Markdown
          </button>
        </Tab>
        <Tab>
          <button class="p-2 bg-blue-500 rounded text-white">
            Preview HTML
          </button>
        </Tab>
      </TabList>
      <TabPanels>
        <TabPanel>
          <textarea
            ref="textarea"
            class="w-full border border-gray-300 p-2 rounded-md"
            v-model="markdownContent"
            cols="30"
            rows="10"
          ></textarea>
        </TabPanel>
        <TabPanel><HtmlViewer :html-content="htmlContent" /></TabPanel>
      </TabPanels>
    </TabGroup>
  </div>
  <div class="absolute bottom-0">
    <button
      class="h-10 bg-pink-500 text-white aspect-square"
      @click="insert(`#`)"
    >
      #
    </button>
    <button
      class="h-10 bg-red-500 text-white aspect-square"
      @click="insert(`-`)"
    >
      -
    </button>
    <button
      class="h-10 bg-yellow-500 text-white aspect-square"
      @click="insert(`*`)"
    >
      *
    </button>
    <button
      class="h-10 bg-lime-500 text-white aspect-square"
      @click="insert(`_`)"
    >
      _
    </button>
    <button
      class="h-10 bg-emerald-500 text-white aspect-square"
      @click="insert(`[`)"
    >
      [
    </button>
    <button
      class="h-10 bg-cyan-500 text-white aspect-square"
      @click="insert(`]`)"
    >
      ]
    </button>
    <button
      class="h-10 bg-blue-500 text-white aspect-square"
      @click="insert(`(`)"
    >
      (
    </button>
    <button
      class="h-10 bg-purple-500 text-white aspect-square"
      @click="insert(`)`)"
    >
      )
    </button>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
