<template>
  <div class="container my-5">
    <h1
      style="
        font-weight: 700;
        font-size: 28px;
        text-align: center;
        color: white;
      "
    >
      ToDo App
    </h1>
    <form class="row container my-4" @submit="save">
      <div class="col-md-3"></div>
      <div class="col-md-6" style="text-align: left">
        <label
          for="todo"
          style="font-weight: 700; font-size: 15px; color: white"
          >New ToDo</label
        >
        <input
          class="form-control"
          name="todo"
          id="todo"
          type="text"
          style="
            background-color: transparent;
            border: 2px solid hsla(0, 0%, 100%, 0.35);
            color: inherit;
            height: 48px;
            color: white;
          "
          required
          v-model="todo"
        />
      </div>
      <div class="col-md-3"></div>
      <div class="col-md-3"></div>
      <div class="col-md-6 my-2 d-grid gap-2">
        <button
          type="submit"
          style="
            height: 48px;
            box-shadow: none;
            outline: none;
            padding-left: 12px;
            padding-right: 12px;
            border-radius: 6px;
            font-size: 18px;
            margin-top: 6px;
            margin-bottom: 12px;
            cursor: pointer;
            background-color: #a0a4d9;
            border: 1px solid #a0a4d9;
            color: #1f2023;
            font-weight: 700;
          "
        >
          Add ToDo
        </button>
      </div>
      <div class="col-md-3"></div>
    </form>
    <div class="row">
      <div class="col-md-3"></div>
      <div class="col-md-6">
        <h2
          style="
            font-size: 22px;
            border-bottom: 2px solid hsla(0, 0%, 100%, 0.35);
            padding-bottom: 6px;
            color: white;
            margin-left: 15px;
            margin-right: 30px;
            text-align: left;
          "
        >
          ToDo List
        </h2>
      </div>
      <div class="col-md-3"></div>
    </div>
    <div class="container" v-if="ToDo_list.length">
      <div class="row">
        <div class="col-md-3"></div>
        <div class="col-md-6">
          <ul style="padding: 10px">
            <li
              v-for="(todo, index) in ToDo_list"
              v-bind:key="index"
              style="
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding: 12px 24px;
                border-radius: 6px;
                margin-bottom: 12px;
                margin-right: 15px;
                color: #fff;border: 2px solid hsla(0, 0%, 100%, 0.35);
              "
            >
            <div class="col-md-9" style="text-align:left;">
                              <span
                style="cursor: pointer"
                :class="{ done: todo.done }"
                >{{ todo.todo }}</span
              >

            </div>
            <div class="col-md-2">
            <span class="form-check form-switch" @click="doneTodo(todo)" style="margin-left:20px;">
  <input class="form-check-input" type="checkbox" role="switch" id="flexSwitchCheckDefault" data-onstyle="#1f2023">
              </span>

            </div>
            <div class="col-md-1">
                              <button
                @click="delete_ToDo(index)"
                style="
                  box-shadow: none;
                  outline: none;
                  padding-left: 6px;
                  padding-right: 6px;
                  border-radius: 6px;
                  font-size: 12px;
                  cursor: pointer;
                  background-color: #a0a4d9;
                  border: 1px solid #a0a4d9;
                  color: #1f2023;
                  font-weight: 700;
                "
              >
                Remove
              </button>

            </div>            
            </li>
          </ul>
        </div>

        <div class="col-md-3"></div>
      </div>
    </div>
    <div class="container" v-else>
      <ul></ul>
      <h4
        style="
          display: block;
          margin-block-start: 1.33em;
          margin-block-end: 1.33em;
          margin-inline-start: 0px;
          margin-inline-end: 0px;
          font-weight: bold;
          color: #fff;
        "
      >
        Empty List.
      </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      ToDo_list: [],
    };
  },
  mounted() {
    if (localStorage.getItem("allToDo")) {
      this.ToDo_list = JSON.parse(localStorage.getItem("allToDo"));
    }
  },
  methods: {
    save() {
      var existingTasks = JSON.parse(localStorage.getItem("allToDo"));
      if (existingTasks == null) existingTasks = [];
      localStorage.setItem(
        "ToDO",
        JSON.stringify({ todo: this.todo, done: false })
      );
      existingTasks.push({ todo: this.todo, done: false });
      localStorage.setItem("allToDo", JSON.stringify(existingTasks));
    },
    delete_ToDo(index) {
      this.ToDo_list.splice(index, 1);
      localStorage.setItem("allToDo", JSON.stringify(this.ToDo_list));
    },
    doneTodo(todo) {
        todo.done = !todo.done;
    },
  },
};
</script>
