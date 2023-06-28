<template>
  <div class="list">
    <div class="todoDarkLight">
      <h1>TODO</h1>
      <div class="image-toggle" @click="toggleMode">
        <ImageToggleComponent :mode="mode" @update:mode="updateMode" />
      </div>
    </div>
    <div class="card inputTodo">
      <input type="checkbox" @click="addTodo()" name="newTodo" id="newTodo" />
      <input
        type="text"
        v-model="newTodo.todo"
        placeholder="Create a new todo..."
        @keyup.enter="addTodo()"
      />
    </div>
    <div class="card">
      <draggable v-model="filteredItems" :options="dragOptions" tag="ul">
        <template #item="{ element: item, index }">
          <li
            :key="item.id"
            @mouseover="hoverIndex = index"
            @mouseleave="hoverIndex = -1"
            @click="toggleItemDone(item, $event)"
            class="listItem"
          >
            <input type="checkbox" v-model="item.done" name="todoItem" :id="'item-' + item.index" />
            <label
              :class="{ done: item.done }"
              :for="'item-' + item.index"
              @click.prevent="toggleItemDone(item)"
            >
              {{ item.todo }}
            </label>

            <img
              src="../assets/img/icon-cross.svg"
              alt="cross"
              @click.stop="removeTodo(index)"
              v-show="hoverIndex === index"
            />
          </li>
        </template>
      </draggable>
        <li class="bottom">
          <h3 class="itemsLeft">{{ list.length }} items left</h3>
          <div class="selection notMob">
            <h3 :class="{ active: filter === 'All' }" @click="updateFilter('All')">All</h3>
            <h3 :class="{ active: filter === 'Active' }" @click="updateFilter('Active')">Active</h3>
            <h3 :class="{ active: filter === 'Completed' }" @click="updateFilter('Completed')">
              Completed
            </h3>
          </div>
          <h3 @click="clear()">Clear Completed</h3>
        </li>
        <div class="spacer"></div>
        <div class="selectionMobile">
          <div class="selection">
            <h3 :class="{ active: filter === 'All' }" @click="updateFilter('All')">All</h3>
            <h3 :class="{ active: filter === 'Active' }" @click="updateFilter('Active')">Active</h3>
            <h3 :class="{ active: filter === 'Completed' }" @click="updateFilter('Completed')">
              Completed
            </h3>
          </div>
        </div>
      </div>
      <div class="drag">
        <h2>Drag and drop to reorder list</h2>
      </div>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
import ImageToggleComponent from './imageToggleComponent.vue'
export default {
  name: 'listComponentDark',
  components: {
    draggable,
    ImageToggleComponent
  },
  data() {
    return {
      list: [],
      newTodo: {},
      hoverIndex: -1,
      mode: 'dark',
      filter: 'All',
      filteredItems: [],
      dragOptions: {
        animation: 150
      }
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodo.todo) {
        this.newTodo.done = false
        this.list.push(this.newTodo)
        this.newTodo = {}
        localStorage.setItem('Todo', JSON.stringify(this.list))
      } else {
        alert('Please insert a task')
      }
    },
    clear: function () {
      var count = 0
      while (count <= this.filteredItems.length) {
        this.list.forEach((element) => {
          if (element.done) {
            var i = this.list.indexOf(element)
            this.list.splice(i, 1)
            count += 1
          } else {
            count += 1
          }
        })
      }
    },
    removeTodo: function (index) {
      this.list.splice(index, 1)
    },
    updateFilter: function (filter) {
      this.filter = filter
      switch (filter) {
        case 'All':
          this.filteredItems = this.list
          break
        case 'Active':
          this.filteredItems = this.list.filter((item) => !item.done)
          break
        case 'Completed':
          this.filteredItems = this.list.filter((item) => item.done)
          break
        default:
          this.filteredItems = this.list
      }
    },
    toggleItemDone: function (item, event) {
      if (event.target.tagName.toLowerCase() !== 'input') {
        item.done = !item.done
      }
    },
    toggleMode() {
      this.mode = this.mode === 'dark' ? 'light' : 'dark'
      this.$emit('update:mode', this.mode)
    }
  },
  computed: {
    filteredList: function () {
      return this.filteredItems || this.list
    }
  },
  created() {
    this.list = localStorage.getItem('Todo') ? JSON.parse(localStorage.getItem('Todo')) : this.list
    this.updateFilter(this.filter)
  },
  updated() {
    localStorage.setItem('Todo', JSON.stringify(this.list))
  }
}
</script>
<style scoped lang="scss">
.list {
  display: flex;
  flex-direction: column;
  position: absolute;
  gap: 10px;
  width: 35%;
  top: 35%;
  left: 50%;
  z-index: 2;
  transform: translate(-50%, -20%);
  .todoDarkLight {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-bottom: 50px;
    h1 {
      color: hsl(0, 0%, 98%);
      letter-spacing: 20px;
      font-size: 2.5rem;
    }
    img {
      cursor: pointer;
    }
  }
  .inputTodo {
    display: flex;
    align-items: center;
    margin: 0;
    input[type='checkbox'] {
      color: hsl(235, 19%, 35%);
      appearance: none;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      border: 1px solid hsl(234, 11%, 52%);
      outline: none;
      cursor: pointer;
      margin: 10px 20px 10px 20px;
      &:checked {
        background-color: none;
        background-size: cover;
        background-position: center;
      }
    }
    input[type='text'] {
      width: 100%;
      border: none;
      outline: none;
      height: 50px;
      border-radius: 10px;
      font-size: larger;
      background-color: hsl(237, 14%, 26%);
      color: hsl(0, 0%, 98%);
      ::placeholder {
        color: hsl(236, 9%, 61%);
      }
    }
  }

  .card {
    justify-content: center;
    border-radius: 10px;
    background-color: hsl(237, 14%, 26%);
    ul {
      width: 100%;
      padding: 0;
    }
    .listItem {
      display: flex;
      align-items: center;
      list-style-type: none;
      font-size: larger;
      padding: 10px 0 10px 0;
      border-bottom: 1px solid hsl(234, 11%, 52%);
      color: hsl(234, 39%, 85%);
      cursor: pointer;
      .done {
        text-decoration: line-through;
        color: hsl(236, 9%, 61%);
      }
      input[type='checkbox'] {
        color: hsl(235, 19%, 35%);
        appearance: none;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 1px solid hsl(234, 11%, 52%);
        outline: none;
        cursor: pointer;
        margin: 10px 20px 10px 20px;
        &:checked {
          background-color: hsl(192, 100%, 67%);
          background-image: url(../assets/img/icon-check.svg);
          background-size: cover;
          background-position: center;
        }
      }
      img {
        margin-left: auto;
        padding-right: 30px;
        cursor: pointer;
      }
    }
  }

  .bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    list-style-type: none;
    margin: 0 10px;
    height: 50px;
    h3 {
      font-size: small;
      color: hsl(236, 9%, 61%);
    }
    h3:not(.itemsLeft) {
      cursor: pointer;
    }
    .selection {
      display: flex;
      gap: 10px;
    }
    .active {
      color: hsl(220, 98%, 61%);
    }
  }.selectionMobile {
    display: none;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    margin: 0 10px -10px;
    height: 80px;
    h3 {
      font-size: medium;
      color: hsl(236, 9%, 61%);
    }
    .active {
      color: hsl(220, 98%, 61%);
    }
    .selection {
      display: flex;
      gap: 30px;
    }
  }

  .spacer {
    height: 20px;
    background-color: hsl(235, 21%, 11%);
    display: none;
  }
  .drag{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
    font-size: 0.5em;
    color: hsl(234, 11%, 52%);
  }
}

@media (max-width: 1007px) {
  .list {
    width: 90%; // Ajuste a largura para se adaptar a telas menores
    top: 50%; // Ajuste a posição vertical
    transform: translate(-50%, -50%);
    .bottom{
      padding: 0 10px;
    }
    .selectionMobile{
      display: flex;
    }
    .spacer{
      display: block;
    }
    .notMob h3{
      display: none;
    }
  }
}
</style>
