<template>
  <div class="modalcart">
    <b-modal id="modalshow" hide-footer size="lg">
      <div class="wrapmodal">
        <div class="container">
          <div class="bg0 p-t-60 p-b-30 p-lr-15-lg how-pos3-parent">
            <b-row>
              <b-col lg="6">
                <b-card
                  v-bind:src="
                          'http://127.0.0.1:8000/uploads/product/'+img"
                  img-alt="Image"
                  style="max-width: 20rem"
                >
                </b-card>
              </b-col>
              <b-col lg="6">
                <h4>{{name}}</h4>
                <b-badge pill variant="light">{{price}}</b-badge>
                <div class="choose">
                  <b-form-select
                    class="size"
                    v-model="selected"
                    :options="size"
                  ></b-form-select>
                  <b-form-select
                    class="color"
                    v-model="selecteds"
                    :options="color"
                  ></b-form-select>
                  <b-form-spinbutton
                    class="count"
                    id="demo-sb"
                    v-model="value"
                    min="1"
                    max="50"
                  ></b-form-spinbutton>
                  <div class="actions">
                  <b-button class="addtocart" pill variant="info" @click="addItemToCart(product)">Add to cart</b-button>
                  <b-button class="buynow" pill variant="info" @click="addItemToCart(product)">Buy now</b-button>
                  </div>
                </div>
                  <b-card-text>
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </b-card-text>
              </b-col>
            </b-row>
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
import Swal from "sweetalert2";
export default {
  data() {
    return {
      product:{
        id:null
      },

      img:null,
      name:null,
      price:null,

      value: 1,
      selected: null,
      size: [
        { value: null, text: "Choose size" },
        { value: "1", text: "Size 37" },
        { value: "2", text: "Size 38" },
        { value: "3", text: "Size 39" },
        { value: "4", text: "Size 40 " },
        { value: "5", text: "Size 41 " },
        { value: "6", text: "Size 42 " },
        { value: "7", text: "Size 43 " },
      ],
      selecteds: null,
      color: [
        { value: null, text: "Choose color" },
        { value: "a", text: "Black" },
        { value: "b", text: "White" },
        { value: "c", text: "Red" },
        { value: "d", text: "Blue" },
        { value: "e", text: "Orange" },
      ],
    };
  },
  created(){
  },
  methods: {
    addItemToCart(product){
      this.cart.push(product);
      console.log(this);
    },
    
    getDetail() {
      var self = this;
      Vue.axios
        .get("http://127.0.0.1:8000/api/product/"+id)
        .then(function(resp) {
          self.name = resp.data.data.name;
          self.price = resp.data.data.import_price;
          self.img = resp.data.data.img;
          console.log("Data:", resp.data.data);
        })
        .catch(function(error) {
          console.log("Loi:", error);
        });
    }
  }
};
</script>

<style scoped>
.col-3 {
  -ms-flex: 0 0 25%;
  -webkit-box-flex: 0;
  flex: 0 0 25%;
  max-width: 25%;
  padding: 15px 10px;
}
.modal .modal-content .modal-body {
  padding-top: 24px;
  padding-right: 24px;
  padding-bottom: 16px;
  padding-left: 24px;
  line-height: 1.9;
  height: 600px;
}
.modal .modal-content {
  margin: 0px 20px;
}
.choose {
  padding: 10px 10px;
  margin: 10px 50px;
  width: 200px;
}
.size {
  margin: 10px;
}
.color {
  margin: 10px;
}
.count {
  margin: 10px;
}
.addtocart{
    margin: 10px 38px;
}
.actions{
    display: inline-block;
}
</style>