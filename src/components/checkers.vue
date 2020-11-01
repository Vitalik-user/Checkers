<template>
  <div>
    <button>Color</button>
  <div class="desk">
    <div v-on:click="getCoord"
         v-for="check of checks"
         :key = 'check.id'
         v-if="check.itVisible"
         v-bind:key="check.id"
         v-bind:style="styles(check)"
         v-bind:class="{checkerWhite:check.color, checkerBlack: !check.color, target: check.target,
         lightBorderWhite:check.lightBorderWhite,lightBorderBlack:check.lightBorderBlack}">
    </div>

  </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      checks: [
        {id: 1,  gridArea: "1 / 1 / 2 / 2", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 2,  gridArea: "1 / 3 / 2 / 4", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 3,  gridArea: "1 / 5 / 2 / 6", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 4,  gridArea: "1 / 7 / 2 / 8", itVisible: true, color: true, target: false, lightBorderWhite: false},

        {id: 5,  gridArea: "2 / 2 / 3 / 3", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 6,  gridArea: "2 / 4 / 3 / 5", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 7,  gridArea: "2 / 6 / 3 / 7", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 8,  gridArea: "2 / 8 / 3 / 9", itVisible: true, color: true, target: false, lightBorderWhite: false},

        {id: 9,   gridArea: "3 / 1 / 4 / 2", itVisible: true, color: true, target: false, lightBorderWhite: false},
        {id: 10,  gridArea: "3 / 3 / 4 / 4", itVisible: false, color: true, target: false, lightBorderWhite: false},
        {id: 11,  gridArea: "3 / 5 / 4 / 6", itVisible: false, color: true, target: false, lightBorderWhite: false},
        {id: 12,  gridArea: "3 / 7 / 4 / 8", itVisible: false, color: true, target: false, lightBorderWhite: false},

        {id: 13,  gridArea: "4 / 2 / 5 / 3", itVisible: false, target: false},
        {id: 14,  gridArea: "4 / 4 / 5 / 5", itVisible: false, target: false},
        {id: 15,  gridArea: "4 / 6 / 5 / 7", itVisible: false, target: false},
        {id: 16,  gridArea: "4 / 8 / 5 / 9", itVisible: false, target: false},


        {id: 17,  gridArea: "5 / 1 / 6 / 2", itVisible: false, target: false},
        {id: 18,  gridArea: "5 / 3 / 6 / 4", itVisible: false, target: false},
        {id: 19,  gridArea: "5 / 5 / 6 / 6", itVisible: false, target: false},
        {id: 20,  gridArea: "5 / 7 / 6 / 8", itVisible: false, target: false},

        {id: 21, gridArea: "6 / 2 / 7 / 3", itVisible: false, color: false, target: false, lightBorderBlack: false},
        {id: 22, gridArea: "6 / 4 / 7 / 5", itVisible: false, color: false, target: false, lightBorderBlack: false},
        {id: 23, gridArea: "6 / 6 / 7 / 7", itVisible: false, color: false, target: false, lightBorderBlack: false},
        {id: 24, gridArea: "6 / 8 / 7 / 9", itVisible: true, color: false, target: false, lightBorderBlack: false},

        {id: 25, gridArea: "7 / 1 / 8 / 2", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 26, gridArea: "7 / 3 / 8 / 4", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 27, gridArea: "7 / 5 / 8 / 6", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 28, gridArea: "7 / 7 / 8 / 8", itVisible: true, color: false, target: false, lightBorderBlack: false},

        {id: 29, gridArea: "8 / 2 / 9 / 3", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 30, gridArea: "8 / 4 / 9 / 5", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 31, gridArea: "8 / 6 / 9 / 7", itVisible: true, color: false, target: false, lightBorderBlack: false},
        {id: 32, gridArea: "8 / 8 / 9 / 9", itVisible: true, color: false, target: false, lightBorderBlack: false},

      ],
      borderNone: 'none',
      border: '4px solid red',
      lightBorder: false,
      gridArea: String
    }
  },
  methods:{
    getCoord(event) {
      let previousItem = this.gridArea
      this.gridArea = event.target.style.gridArea
      this.getlightBorderWhite(this.gridArea)
      if(this.lightBorder) {
        this.moveDown(previousItem)
      }else {
        for (let check of this.checks) {
          if (check.lightBorderBlack && check.itVisible) {
            check.lightBorderBlack = false
            check.itVisible = false
          }
          if (check.lightBorderWhite && check.itVisible) {
            check.lightBorderWhite = false
            check.itVisible = false
          }
          if(check.target) {
            check.target = false
          }
          if (this.gridArea == check.gridArea) {
            check.target = true
          }
        }
        this.showMoveDown()
      }
    },
    showMoveDown(){
      for (let i = 0, kol = 0; i < this.checks.length; i += 4, kol++) {
        for (let k = i, count = 0; k < (i + 4); k++, count++) {
          if (kol % 2) {
            if (count == 3) {
              if (this.gridArea == this.checks[k].gridArea) {
                if (!this.checks[k + 4].itVisible) {
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 4].itVisible = true
                }
              }
            } else {
              if (this.gridArea == this.checks[k].gridArea) {
                if (this.checks[k + 4].itVisible && !this.checks[k + 5].itVisible) {
                  this.checks[k + 5].lightBorderWhite = true
                  this.checks[k + 5].itVisible = true
                } else if (!this.checks[k + 4].itVisible && this.checks[k + 5].itVisible) {
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 4].itVisible = true
                } else if (!this.checks[k + 4].itVisible && !this.checks[k + 5].itVisible) {
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 5].lightBorderWhite = true
                  this.checks[k + 4].itVisible = true
                  this.checks[k + 5].itVisible = true
                }
              }
            }
          } else {
            if (count == 0) {
              if (this.gridArea == this.checks[k].gridArea) {
                if (!this.checks[k + 4].itVisible) {
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 4].itVisible = true
                }
              }
            } else {
              if (this.gridArea == this.checks[k].gridArea) {
                if (this.checks[k + 3].itVisible && !this.checks[k + 4].itVisible) {
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 4].itVisible = true
                } else if (!this.checks[k + 3].itVisible && this.checks[k + 4].itVisible) {
                  this.checks[k + 3].lightBorderWhite = true
                  this.checks[k + 3].itVisible = true
                } else if (!this.checks[k + 3].itVisible && !this.checks[k + 4].itVisible) {
                  this.checks[k + 3].lightBorderWhite = true
                  this.checks[k + 4].lightBorderWhite = true
                  this.checks[k + 3].itVisible = true
                  this.checks[k + 4].itVisible = true
                }
              }
            }
          }
        }
      }
    },
    moveDown(previousItem){
      for (let check of this.checks) {
        if (check.lightBorderWhite && check.itVisible) {
          check.lightBorderWhite = false
          check.itVisible = false
        }
        if (this.gridArea == check.gridArea) {
          check.itVisible = true
          check.color = true
        }
        if (previousItem == check.gridArea) {
          check.itVisible = false
        }
      }
    },
    showMoveUp(){
      for (let i = this.checks.length - 1, kol = 0; i > 0; i -= 4, kol++) {
        for (let k = i, count = 0; k > (i - 4); k--, count++) {
          if (kol % 2) {
            if (count == 3) {
              if (this.gridArea == this.checks[k].gridArea) {
                if (!this.checks[k - 4].itVisible) {
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 4].itVisible = true
                }
              }
            } else {
              if (this.gridArea == this.checks[k].gridArea) {
                if (this.checks[k - 4].itVisible && !this.checks[k - 5].itVisible) {
                  this.checks[k - 5].lightBorderBlack = true
                  this.checks[k - 5].itVisible = true
                } else if (!this.checks[k - 4].itVisible && this.checks[k - 5].itVisible) {
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 4].itVisible = true
                } else if (!this.checks[k - 4].itVisible && !this.checks[k - 5].itVisible) {
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 5].lightBorderBlack = true
                  this.checks[k - 4].itVisible = true
                  this.checks[k - 5].itVisible = true
                }
              }
            }
          } else {
            if (count == 0) {
              if (this.gridArea == this.checks[k].gridArea) {
                if (!this.checks[k - 4].itVisible) {
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 4].itVisible = true
                }
              }
            } else {
              if (this.gridArea == this.checks[k].gridArea) {
                if (this.checks[k - 3].itVisible && !this.checks[k - 4].itVisible) {
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 4].itVisible = true
                } else if (!this.checks[k - 3].itVisible && this.checks[k - 4].itVisible) {
                  this.checks[k - 3].lightBorderBlack = true
                  this.checks[k - 3].itVisible = true
                } else if (!this.checks[k - 3].itVisible && !this.checks[k - 4].itVisible) {
                  this.checks[k - 3].lightBorderBlack = true
                  this.checks[k - 4].lightBorderBlack = true
                  this.checks[k - 3].itVisible = true
                  this.checks[k - 4].itVisible = true
                }
              }
            }
          }
        }
      }


    },
    moveUp(previousItem){
      for (let check of this.checks) {
        if (check.lightBorderBlack && check.itVisible) {
          check.lightBorderBlack = false
          check.itVisible = false
        }
        if (this.gridArea == check.gridArea) {
          check.itVisible = true
          check.color = false
        }
        if (previousItem == check.gridArea) {
          check.itVisible = false
        }
      }
    },
    getlightBorderWhite(gridArea){
      for(let check of this.checks){
        if(gridArea == check.gridArea){
          this.lightBorder = check.lightBorderWhite
        }
      }
    },
    styles(check) {
      return {
          gridArea: check.gridArea,
          border: check
        }
    }

  },
}
</script>

<style scoped>
.desk{
  display: grid;
  background:url("../assets/desk.jpg") no-repeat;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(8,1fr);
  width: 435px;
  height: 432px;
  margin:  auto;

}
.checkerWhite{

  background: url("../assets/white.png") no-repeat center center;
}

.checkerBlack {
  background: url("../assets/black.png") no-repeat center center;
}

.target{
  border: 4px solid red;
}
.lightBorderWhite{
  background: url("../assets/white.png") no-repeat center center;
  opacity: 0.5;
}
.lightBorderBlack{
  background: url("../assets/black.png") no-repeat center center;
  opacity: 0.5;
}

</style>