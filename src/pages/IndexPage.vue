<template>
  <q-page>
    <div class="q-mt-sm flex justify-center">
      <q-input
        rounded
        standout
        v-model="todoTask"
        label="Task Details"
        style="width: 400px"
        @keydown.enter="addItem"
      >
        <template v-slot:after>
          <q-btn
            dense
            round
            color="primary"
            class="text-h6 bi bi-plus"
            label="+"
            @click="addItem"
          />
        </template>
      </q-input>
    </div>
    <div
      class="row justify-center q-my-sm"
      v-for="(item, index) in todoList"
      :key="index"
    >
      <q-card
        v-if="todoList.length > 0"
        class="my-card text-white"
        style="
          background: radial-gradient(circle, #35a2ff 0%, #014a88 100%);
          width: 400px;
        "
      >
        <q-card-section>
          <div class="col-8 q-pt-none">{{ item.task }}</div>
          <div class="col-auto q-py-md">
            <q-btn dense round icon="done" @click="remove(index)" />
          </div>
        </q-card-section>
      </q-card>
    </div>
    <!-- wanted to use v-if & else on the q-card-section, however todoList.length>0 was always true. Hence the seperate div-->
    <div class="justify-center q-mt-lg" v-if="todoList.length == 0">
      <div class="text-center">No to-dos here, enjoy a meme instead</div>
      <div class="row justify-center">
        <q-img
          class="justify-center"
          rounded
          src="~/assets/completedToDos.jpg"
          style="width: 400px"
        />
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      todoTask: "",
      todoList: [
        { task: "Create a todo" },
        {
          task: "Something else This is a abunch of text just to exceed the 400px I set to see how thetext wrapping will look like this, I don't know how it will work but hopefully this is enough letters for me to see what it will look like even when it stacks one line of top of another line to show a full and completely thought out note :)",
        },
      ],
    };
  },
  methods: {
    addItem() {
      // this.todoList.push({ title: this.todoTitle, task: this.todoTask });
      this.todoList.push({ task: this.todoTask });
      this.todoTask = "";
    },
    remove(index) {
      this.todoList.splice(index, 1);
    },
  },
});
</script>
