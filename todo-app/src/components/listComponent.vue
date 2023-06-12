<template>
  <div class="list">
    <h1>TODO</h1>
    <div class="card">
      <input type="text" />
    </div>
    <div class="card">
      <ul>
        <li v-for="item in list" :key="item.id">
          <input type="checkbox" name="todoItem" id="'item-'+ item.id" checked />
          <label for="'item-' + item.id">
            {{ item.todo }}
          </label>
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
        { todo: 'Estudar', status: 'waiting' },
        { todo: 'Trabalhar', status: 'done' },
        { todo: 'Cortar Grama', status: 'waiting' },
        { todo: 'Exercitar', status: 'done' },
        { todo: 'Lavar a roupa', status: 'waiting' },
        { todo: 'Cozinhar', status: 'done' }
      ]
    }
  }
}
</script>
<style scoped lang="scss">
.list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 35%;

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
    }
    input[type='text'] {
      width: 80%;
      border: none;
      outline: none;
      height: 50px;
      font-size: larger;
    }
  }
}
</style>
