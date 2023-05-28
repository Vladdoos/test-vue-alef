<template>
  <footer>
    <p>all rights reserved</p>
  </footer>
</template>

<script>
export default {
  name: "footerBlock"
}
</script>

<style scoped>
footer{
  display: flex;
  justify-content: center;
  background: #FAFAFA;
  box-shadow: 0 1px 0 rgba(17, 17, 17, 0.1);
  padding: 30px 0;
}
footer p {
  margin: 0;
  font-style: normal;
  font-weight: 400;
  font-size: 13px;
  line-height: 16px;
  color: #000000;
}
</style>
