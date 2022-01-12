<template>
  <div id="appErr">
    <div class="gradient-border" id="box">
      <center>
        Sorry, But <br />
        There're <br />
        Nothing Here
      </center>
    </div>
    <br>
    &lt; <a @click="$router.go(-1)" class="b-link">Go back</a>
  </div>
</template>

<style>
  @import url(./error.css);
</style>