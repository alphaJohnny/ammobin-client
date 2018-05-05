<template>
<form>
  <h3> to celibrate 1 year of ammobin.ca existing. enter draw for free stickers. must be canadian address. limit of X.</h3>
  <div>
    <label>name</label>
    <input type="text" required />
  </div>

  <div>
    <label>address</label>
    <input type="text" required />
  </div>

  <div>
    <label>province</label>
    <input type="text" required />
  </div>

  <div>
    <label>postal</label>
    <input type="text" required />
  </div>

  <div>
    <label>name</label>
    <input type="text" required />
  </div>

  <div>
    <label>thoughts about ammobin.ca</label>
    <input type="text" required />
  </div>
  <div> disclaimer. link to api source. records will be destroyed once completed

  </div>
</form>
</template>

<script>
import { provinces2Char } from "./provinces";

export default {
  data: {
    provinces: [null].concat(provinces2Char)
  },
  methods: {
    submit(e) {
      //todo: post to api
    }
  }
};
</script>
