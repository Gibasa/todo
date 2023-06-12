<template>
  <div class="list">
    <h1>TODO</h1>
    <div class="card">
      <input type="text" />
    </div>
    <div class="card">
      <ul>
        <li>a</li>
        <li>b</li>
        <li>c</li>
        <li>d</li>
        <li>e</li>
      </ul>
    </div>
  </div>
</template>
<style scoped lang="scss">
.list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 35%;
}
.card{
    display: flex;
    justify-content: center;
    border-radius: 10px;
    background-color: hsl(0, 0%, 98%);
    
    input{
        width: 80%;
        border: none;
        outline: none;
        height: 50px;
    }
}
</style>
