<template>
<!-- eslint-disable vue/valid-v-model --> 
  <div class="container">
    <div class="sample">
        <div class="Mednikov-class"> 
            <h2 class="Mednikov-text">
                СОЗДАНИЕ ПИРОГА
            </h2> 
        </div>
        <hr>
        <div class="x" style="text-align: left"> 
            <button type="button"
                    class="btn btn-primary"
                    @click="addLayer"
            >
        
          Добавить слой
        </button>
        </div>
        <hr>
        <div class="row">
            <div class="col pickImg">
                <div class="cake">
                    <div 
                        class="layer"
                        :class="'layer-' + layer.type"
                        :style="{height: layer.height * 10 + 'px'}"
                        v-for="(layer, i) in layers"
                        v-bind:key = layer.id 
                        @click="changeHeight(i, 1)"
                        @contextmenu.prevent="changeHeight(i, -1)"
                        >
                    </div>
                </div>
            </div>
            <div class="col col-sn-6">
                <table class="table table-bordered">
                    <tr>
                        <th>Вид</th>
                        <th>Высота</th>
                        <th>Убрать</th>
                    </tr>
                    <tr 
                        v-for="(layer, i) in layers"
                        v-bind:key = layer.id 
                     >
                        <td>
                            <select class="form-control selectColor" v-model="layers[i].type">
                                <option :value="key" 
                                        v-bind:key = key
                                        v-for="(lt, key) in layersTypes">
                                    {{ lt.label }}
                                </option>
                            </select>
                        </td>
                        <td>
                            <input 
                                class="form-control"
                                type="text"
                                min="0"
                                max="10"
                                v-model.number="layers[i].height"
                                @input="updateValue($event, i)"
                                >
                        </td>
                        <td>
                            <button type="button"
                            class="btn btn-danger"
                            @click="deleteLayer(i)"
                            >
                        -
                        </button>    
                        </td>
                    </tr>
                </table>
            </div>
        </div>
        <hr>
        <div class="alert alert-success price">
            <span class="price">
                {{ price }}
                руб. 
            </span>
            <button type="button"
                    class="btn btn-warning">
                Заказать сейчас!
            </button>
        </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
        layers: [],
        layersTypes: {
            biscuit: {
                pricelsm: 50,
                label: 'Бисквит'
            },
            beze: {
                pricelsm: 100,
                label: 'Безе'
            },
            curd: {
                pricelsm: 60,
                label: 'Творожный'
            }
        },
        defaultLayerType: 'biscuit',
        defaultHeight: 4,
    }
  },
  computed: {
      price() {
          let sum=0;
          this.layers.forEach((layer)=> {
              sum += layer.height * this.layersTypes[layer.type].pricelsm;
          });
          return sum;
      }
  },
  methods: {
    addLayer(){
        if (this.layers.length > 6) { return }
        this.layers.push({
            id: Date.now(),
            type: this.defaultLayerType,
            height: this.defaultHeight
        }); 
    },
    updateValue(event, i) {
      const value = event.target.value
      if (String(value).length > 2  || value.indexOf('-') != -1 ) {
        this.layers[i].height = 1
      }
      if(value > 10 || value == "00" ) {
          this.layers[i].height = 1
      }
      this.$forceUpdate()
    },
    changeHeight(i, dh){
        this.layers[i].height += dh;
    },
    deleteLayer(i){
        this.layers.splice(i, 1);
    }
  }
}
</script>

<style>
.Mednikov-class {
    background-color: darkorange;
}
.Mednikov-text {
    color: white;
    text-align: center;
    margin-left: 20px;
}
.btn {
    background-color: white;
    color: black;
    border-radius: 5px;
}
.btn.btn-primary {
    border: orange solid 1px;
    margin-left: 20px;
}
.btn.btn-danger {
    border: red solid 1px;
}

.table.table-bordered th, .table.table-bordered td {
    border: black 1px solid;
    width: 150px;
    text-align: left;
    padding-left: 5px;
}
input, select {
    width: 143px;
}
.selectColor {
    color:whitesmoke;
    background:orange;
}
.table.table-bordered {
    border-collapse: collapse;
    display: inline-grid;
}
.layer {
    transition: height 0.5s;
}
.layer-biscuit {
    background: url('../images/biscuit.jpg')
}
.layer-beze {
    background: url('../images/beze.jpg')
}
.layer-curd {
    background: url('../images/curd.jpg')
}
.price{
    font-size: 26px;
    margin-right: 40px;
}
.pickImg {
    width: 500px;
    margin-left: 20px;
    margin-right: 20px;
}
.row {
    display: flex;
}
</style>