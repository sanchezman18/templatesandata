<template>
<div class="container-fluid">
  <!--<div class="bg-primary text-white m-2 p-3">
    <h3 v-bind:data-size="size" class="display-4">Product: {{name}} </h3>
  </div>-->
  <!--
  <h2 class="bg-primary text-white text-center p-3">{{message}}</h2>
  <input class= "form-control bg-light" placeholder="Type here..."
    v-on:keydown.ctrl="handleKey"
  />
  
  <table class="table table-sm table-bordered table-striped text-left">
    <tr> <th>Name</th><th>Price</th><th>Actions</th> </tr>
    <tbody>
      <tr v-for="p in pageItems" v-bind:key="p.name" v-bind:odd="i % 2 == 0" >
        
        <td>{{p.name}}</td>
        <td>{{p.price}}</td>
        <td>
           <button class="btn btn-sm bg-primary text-white"
            v-on="buttonEvents"
            v-bind:data-name="p.name" >
            Select 
          </button>
        </td>
      </tr>
    </tbody>
  </table> 
  <button v-for="i in pageCount"  v-bind:key="i" v-on:click="selectPage(i)" 
    class="btn btn-secondary m-1"
    v-bind:class="{'bg-primary': currentPage == i}">
    {{i}}
  </button>-->
  <div class="bg-info m-2 p-2 text-white">
   <div> Value: {{dataValue}} </div>
   <div> Other value {{otherValue || "(Empty)" }}  </div>
   <div> Name: {{name}} </div>

    </div>
  

  <div class="bg-primary m-2 p-2 text-white">
  <div class="form-check">
    <label class="form-check-label">
      <input class="form-check-input" type="checkbox"
            v-model="dataValue"
      />
      Data value
    </label>
  </div>
  </div>

<div class="bg-primary m-2 p-2">
  <input type="text" class="form-control" v-model="otherValue"/>
</div>

<div class="bg-primary m-2 p-2">
<div class="form-group">
  <label>Selected Names</label>
  <select class="form-control" v-model="name" >
    <option value="all">Everyone</option>
    <option v-for="n in otherNames" v-bind:key="n" v-bind:value="n" >Just {{n}} </option>
  </select>
</div>
</div>

  <div class="text-center m-2">
    <button class="btn btn-secondary" v-on:click= "reset">
      Reset
    </button>
  </div>
</div>
</template>

<script>


export default {
  name: 'App',
  data: function () {
    return {
      dataValue: false,
      pageSize: 3,
      currentPage: 1,
      message: "Products",
      otherValue: "",
      name: "Sasha",
      otherNames: ["Artem", "Nikita", "Max", "Ivan"],
      buttonEvents: {
        click: this.handleClick,
        mousemove: this.handleMouseEvent,
        mouseleave: this.handleMouseEvent
    },
      products: [
        {name: "Kayak" , price: 275},
        {name: "Lifejacket", price: 48.95},
        {name: "Soccer Ball", price: 19.50},
        {name: "Corner Flags", price: 39.95},
        {name: "Stadium", price: 79500},
        {name: "Thinking Cap", price: 16},
        {name: "Unsteady Chair", price: 29.95},
        {name: "Human Chess Board", price: 75},
        {name: "Bling Bling King", price: 1200}
      ]
    }
  },
  computed: {
    pageCount() {
      return Math.ceil(this.products.length / this.pageSize);
    },
    pageItems() {
      let start = (this.currentPage - 1) * this.pageSize;
      return this.products.slice(start, start + this.pageSize)
    }
  },
  methods: {
    selectPage(page) {
      this.currentPage = page;
    },
    handleClick($event) {
      let name = $event.target.dataset.name
      this.message = `Select : ${name}`
    },
    handleMouseEvent($event) {
      let name = $event.target.dataset.name
      if ($event.type == "mousemove") {
        this.message = `Move in ${name} ${this.counter++}`;
      } else {
        this.counter = 0;
        this.message = "Ready";
      }
    },
    handleKey($event) {
      this.message = $event.key;
    },
    reset() {
      this.dataValue = false;
      this.otherValue = "";
    },
    handleChange($event) {
      //this.dataValue = $event.target.checked;
      if($event.target.type === "checkbox") {
        this.dataValue = $event.target.checked
      }else{
        this.otherValue = $event.target.value
      }
    }
  },
  filters: {
    currency(value) {
      return new Intl.NumberFormat("en-US",
      { style: "currency", currency: "USD"}).format(value);
    }
  }
  
  
}  // p317
</script> 

<style>
[odd]{ background-color: aqua; }  
</style>