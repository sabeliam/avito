<template>
  <header>
    <div class="container-fluid">
      <div class="row">
        <div class="logo col-md-3">
          <h3>AVITO</h3>
        </div>
        <div class="navbar col-md-9">
          <!-- <span class="search">
            <input type="text" @change="$emit('typing', $event.target.value)"/>
            <button type="button" class="btn btn-light">search</button>
          </span>-->
          <div class="input-group search">
            <input
              type="text"
              @change="$emit('typing', $event.target.value)"
              class="form-control"
              placeholder="Введите название товара"
            />
            <div class="input-group-append">
              <button class="btn btn-secondary" type="button">search</button>
            </div>
          </div>
          <span class="categories">
            <select @change="$emit('changed', $event.target.value)">
              <option value>Все категории</option>
              <option v-for="category in categories" :key="category" :value="category">{{category}}</option>
            </select>
          </span>
          <!-- <div class="dropdown">
            <button
              class="btn btn-secondary dropdown-toggle"
              type="button"
              id="dropdownMenuButton"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >{{ selectedCategory }}</button>
            <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
              <p class="dropdown-item" @click="$emit('changed', $event.target.value)" v-for="category in categories" :key="category" :value="category">{{category}}</p>
            </div>
          </div> -->
        </div>
      </div>
    </div>
  </header>
</template>


<script>
export default {
  props: ["categories", 'selectedCategory']
};
</script>



<style scoped>
header {
  position: fixed;
  width: 100vw;
  top: 0px;
  z-index: 10;
}
.logo {
  background-color: rgba(107, 128, 199, 0.397);
}
.navbar {
  background-color: rgb(131, 231, 223);
  justify-content: space-around;
}

.search {
  width: 50%;
}
.has-search .form-control {
  padding-left: 2.375rem;
}

.has-search .form-control-feedback {
  position: absolute;
  z-index: 2;
  display: block;
  width: 2.375rem;
  height: 2.375rem;
  line-height: 2.375rem;
  text-align: center;
  pointer-events: none;
  color: #aaa;
}
</style>