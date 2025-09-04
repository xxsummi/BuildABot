<template>
  <div class="content">
    <div class="part-info" id="partInfo"></div>
    <div class="preview">
      <CollabsibleSection>
      <div class="preview-content">
        <div class="top-row">
          <img :src="selectedRobot.head.src"/>
        </div>
        <div class="middle-row">
          <img :src="selectedRobot.leftArm.src" class="rotate-left"/>
          <img :src="selectedRobot.torso.src"/>
          <img :src="selectedRobot.rightArm.src" class="rotate-right"/>
        </div>
        <div class="bottom-row">
          <img :src="selectedRobot.base.src"/>
        </div>
      </div>
      </CollabsibleSection>
      <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
    </div>
      <div class="top-row">
      <PartSelector :parts="availableParts.heads" position="top" @partSelected="part => selectedRobot.head=part"/>
      <!-- <div class="top part" :style="headBorderStyle">
      <div :class="[saleBorderClass, 'top', 'part']">
        <div class="robot-name">
          {{ selectedRobot.head.title }}
          <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
        </div>
        <img :src="selectedRobot.head.src" title="head" />
        <button @click="selectPrevHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div> -->
    </div>
    <div class="middle-row">
      <PartSelector :parts="availableParts.arms" position="left" @partSelected="part => selectedRobot.leftArm=part"/>
      <PartSelector :parts="availableParts.torsos" position="center" @partSelected="part => selectedRobot.torso=part"/>
      <PartSelector :parts="availableParts.arms" position="right" @partSelected="part => selectedRobot.rightArm=part"/>
      <!-- <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm" />
        <button @click="selectPrevLeft()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeft()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="torso" />
        <button @click="selectPrevTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="right arm" />
        <button @click="selectPrevRight()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRight()" class="next-selector">&#9660;</button>
      </div> -->
    </div>
    <div class="bottom-row">
      <PartSelector :parts="availableParts.bases" position="bottom" @partSelected="part => selectedRobot.base=part"/>
      <!-- <div class="bottom part">
        <img :src="selectedRobot.base.src" title="base" />
        <button @click="selectPrevBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div> -->
    </div>
    <div>
      <h2>Cart</h2>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in cart" :key="index">
            <td>{{ robot.head.title }}</td>
            <td class="cost">${{ robot.cost }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/parts';
import PartSelector from './PartSelector.vue';
import CollabsibleSection from '../shared/CollapsibleSection.vue';

// function getPreviousValidIndex(index, length) {
//   const deprecatedIndex = index - 1;
//   return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
// }

// function getNextValidIndex(index, length) {
//   const incrementedIndex = index + 1;
//   return incrementedIndex > length - 1 ? 0 : incrementedIndex;
// }

export default {
  name: 'RobotBuilder',
  components: { PartSelector, CollabsibleSection },
  data() {
    return {
      cart: [],
      availableParts,
      selectedRobot:  { 
        head: {},
        leftArm: {},
        torso: {},
        rightArm: {},
        base: {},
      }
    };
  },
  computed: {
    saleBorderClass() {
      return this.selectedRobot.head.onSale ? 'sale-border' : '';
    },
    headBorderStyle() {
      return this.selectedRobot.head.onSale
        ? { border: '3px solid red' }
        : { border: '3px solid #aaa' };
    },
    // selectedRobot() {
    //   return {
    //     head: {},
    //     leftArm: {},
    //     torso: {},
    //     rightArm: {},
    //     base: {},
    //     // head: this.availableParts.heads[this.selectedHeadIndex],
    //     // leftArm: this.availableParts.arms[this.selectedLeftIndex],
    //     // torso: this.availableParts.torsos[this.selectedTorsoIndex],
    //     // rightArm: this.availableParts.arms[this.selectedRightIndex],
    //     // base: this.availableParts.bases[this.selectedBaseIndex],
    //   };
    // },
  },
  methods: {
    addToCart() {
      // this.$emit('add-to-cart', this.selectedRobot);
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.leftArm.cost + robot.torso.cost + robot.rightArm.cost + robot.base.cost;
      this.cart.push(Object.assign({}, robot, { cost }));
      console.log('Cart:', this.cart);
    }
  }
}
</script>
    // selectNextHead() {
    //   this.selectedHeadIndex = getNextValidIndex(this.selectedHeadIndex, this.availableParts.heads.length);
    // },
    // selectPrevHead() {
    //   this.selectedHeadIndex = getPreviousValidIndex(this.selectedHeadIndex, this.availableParts.heads.length);
    // },
    // selectNextLeft() {
    //   this.selectedLeftIndex = getNextValidIndex(this.selectedLeftIndex, this.availableParts.arms.length);
    // },
    // selectPrevLeft() {
    //   this.selectedLeftIndex = getPreviousValidIndex(this.selectedLeftIndex, this.availableParts.arms.length);
    // },
    // selectNextTorso() {
    //   this.selectedTorsoIndex = getNextValidIndex(this.selectedTorsoIndex, this.availableParts.torsos.length);
    // },
    // selectPrevTorso() {
    //   this.selectedTorsoIndex = getPreviousValidIndex(this.selectedTorsoIndex, this.availableParts.torsos.length);
    // },
    // selectNextRight() {
    //   this.selectedRightIndex = getNextValidIndex(this.selectedRightIndex, this.availableParts.arms.length);
    // },
    // selectPrevRight() {
    //   this.selectedRightIndex = getPreviousValidIndex(this.selectedRightIndex, this.availableParts.arms.length);
    // },
    // selectNextBase() {
    //   this.selectedBaseIndex = getNextValidIndex(this.selectedBaseIndex, this.availableParts.bases.length);
    // },
    // selectPrevBase() {
    //   this.selectedBaseIndex = getPreviousValidIndex(this.selectedBaseIndex, this.availableParts.bases.length);
    // },


<style>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name{
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  background: red;
  color: white;
  font-size: 0.8em;
  padding: 2px 4px;
  margin-left: 10px;
  border-radius: 5px;
}
.content {
  position:relative;
}
.add-to-cart {
  position: absolute;
  /* top: -25px; */
  /* right: 30px; */
  width: 210px;
  background-color: #4CAF50;
  font-size: 16px;
  padding: 3px;
  border: 2px solid #4CAF50;
  color: white; 
  text-align: center;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
  /* border-radius: 12px; */
}
td, th {
  text-align: left;
  padding: 8px;
  padding-right: 20px;
}
.cost {
  text-align: right;
  font-family: monospace;}
.sale-border{
  border: 3px solid red;
}
.preview {
  position: absolute;
  top: -20px;
  right: 0;
  width: 210px;
  height: 210px;
  padding: 5px;
}
.preview-content {
  border: 1px solid #999;
}
.preview img {
  width: 50px;
  height: 50px;
}
.rotate-right {
  transform: rotate(90deg);
}
.rotate-left {
  transform: rotate(-90deg);
}
.part-info {
  position: absolute;
  top: -20px;
  left: 0;
  width: 210px;
  height: 210px;
  padding: 5px;
}
</style>
