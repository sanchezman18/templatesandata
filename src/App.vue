<template>
<div class="container-fluid">
  <div class="m-2 p-2 text-white" v-bind:class="dataValue">
    <div>Value: {{dataValue}}</div>
  </div>

<div class="form-check m-2">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input"
      v-model="dataValue" v-bind:true-value="darkColor"
      v-bind:false-value="ligthColor"/>
      Dark Color 
  </label>

<div class="form-group m-2 p-2 bg-secondary">
  <label>Color</label>
  <select v-model="dataValue" class="form-control" >
    <option v-bind:value="darkColor" >Dark Color</option>
    <option v-bind:value="ligthColor" >Light Color</option>
  </select>

</div>
</div>

<div class="form-check-inline m-2">
  <label class="form-check-label">
    <input type="radio" class="form-check-input"
      v-model="dataValue" v-bind:value="darkColor"
    />
    Dark Color
  </label>
</div>
<div class="form-check-inline m-2">
  <label class="form-check-label">
    <input type="radio" class="form-check-input"
      v-model="dataValue" v-bind:value="ligthColor"
    />
    Light Color
  </label>
</div>

</div>
</template>

<script>
export default {
  name: 'App',
  data: function () {
    return {
      darkColor: "bg-primary",
      ligthColor:"bg-info",
      dataValue: "bg-info",
      //dataValue: false,
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