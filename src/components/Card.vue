<template>
  <div class="card">
    <div class="title">
      <slot name="title"/>
    </div>

    <div class="content">
      <slot name="content"/>
    </div>

    <div class="description">
      <slot name="description"/>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Card'
  }
</script>

<style scoped>
img {
  max-width: 100%;
  display: block;
}
.card {
  border: 1px solid silver;
  border-radius: 8px;
  max-width: 200px;
  margin: 0 5px;
  cursor: pointer;
  box-shadow: 0 1px 3px darkgrey;
  transition: 0.2s;
}
.title, .content, .description {
  padding: 16px;
  text-transform: capitalize;
  text-align: center;
}
.description {
  display: flex;
  align-items: center;
  justify-content: center;
}
.description .tag {
  font-size: 13px;
  margin: 0 4px;
  background-color: #2196F3;
  color: #ffffff;
  padding: 5px 8px;
  line-height: 1em;
  border-radius: 3px;
}
.title, .content {
  border-bottom: 1px solid silver;
}
</style>