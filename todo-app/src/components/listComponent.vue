<template>
  <div class="list">
    <div class="todoDarkLight">
      <h1>TODO</h1>
      <img
        v-if="mode === 'dark'"
        @click="mode = 'light'"
        src="../assets/img/icon-moon.svg"
        alt="moon"
      />
      <img
        v-if="mode === 'light'"
        @click="mode = 'dark'"
        src="../assets/img/icon-sun.svg"
        alt="moon"
      />
    </div>
    <div class="card inputTodo">
      <input type="checkbox" name="newTodo" id="newTodo" />
      <input type="text" placeholder="Create a new todo..." />
    </div>
    <div class="card">
      <ul>
        <li
          v-for="(item, index) in list"
          :key="item.id"
          @mouseover="hoverIndex = index"
          @mouseleave="hoverIndex = -1"
        >
          <input type="checkbox" name="todoItem" :id="'item-' + item.id" checked />
          <label :for="'item-' + item.id">
            {{ item.todo }}
          </label>

          <img src="../assets/img/icon-cross.svg" alt="cross" v-show="hoverIndex === index" />
        </li>
        <li class="bottom">
          <h3 class="itemsLeft">5 items left</h3>
          <div class="selection">
            <h3>All</h3>
            <h3>Active</h3>
            <h3>Completed</h3>
          </div>
          <h3>Clear Completed</h3>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: 'listComponent',
  data() {
    return {
      list: [
        { id: 1, todo: 'Estudar', status: 'waiting' },
        { id: 2, todo: 'Trabalhar', status: 'done' },
        { id: 3, todo: 'Cortar Grama', status: 'waiting' },
        { id: 4, todo: 'Exercitar', status: 'done' },
        { id: 5, todo: 'Lavar a roupa', status: 'waiting' },
        { id: 6, todo: 'Cozinhar', status: 'done' }
      ],
      hoverIndex: -1,
      mode: 'light'
    }
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
      border: 1px solid hsl(236, 33%, 92%);
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
    input[type='text'] {
      width: 100%;
      border: none;
      outline: none;
      height: 50px;
      font-size: larger;
      ::placeholder{
        color: hsl(236, 9%, 61%);
      }
    }
  }

  .card {
    display: flex;
    justify-content: center;
    border-radius: 10px;
    background-color: hsl(0, 0%, 98%);
    ul {
      width: 100%;
      padding: 0;
    }
    li {
      display: flex;
      align-items: center;
      list-style-type: none;
      font-size: larger;
      padding: 10px 0 10px 0;
      border-bottom: 1px solid hsl(233, 11%, 84%);
      color: hsl(235, 19%, 35%);
      input[type='checkbox'] {
        color: hsl(235, 19%, 35%);
        appearance: none;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        border: 1px solid hsl(236, 33%, 92%);
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
    margin: 0 10px;
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
  }
}
</style>
