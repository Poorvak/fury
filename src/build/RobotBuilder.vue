<template>
    <div class="content">
        <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
        <div class="top-row">
            <div class="top part">
                <div class="robot-head-name">
                    {{selectedRobot.head.title}}
                    <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
                </div>
                <img :src="selectedRobot.head.src" title="head"/>
                <button @click="selectPrevHead()" class="prev-selector">&#9668;</button>
                <button @click="selectNextHead()" class="next-selector">&#9658;</button>
            </div>
        </div>
        <div class="middle-row">
            <div class="left part">
                <div class="robot-left-arm-name">
                    {{selectedRobot.leftArm.title}}
                </div>
                <img :src="selectedRobot.leftArm.src" title="left arm"/>
                <button @click="selectPrevLeftArm()" class="prev-selector">&#9650;</button>
                <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
            </div>
            <div class="center part">
                <div class="robot-torso-name">
                    {{selectedRobot.torso.title}}
                </div>
                <img :src="selectedRobot.torso.src" title="left arm"/>
                <button @cloick="selectPrevTorso()" class="prev-selector">&#9668;</button>
                <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
            </div>
            <div class="right part">
                <div class="robot-right-arm-name">
                    {{selectedRobot.rightArm.title}}
                </div>
                <img :src="selectedRobot.rightArm.src" title="left arm"/>
                <button @click="selectPrevRightArm()" class="prev-selector">&#9650;</button>
                <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
            </div>
        </div>
        <div class="bottom-row">
            <div class="bottom part">
                <div class="robot-base-name">
                    {{selectedRobot.base.title}}
                </div>
                <img :src="selectedRobot.base.src" title="left arm"/>
                <button @click="selectPrevBase()" class="prev-selector">&#9668;</button>
                <button @click="selectNextBase()" class="next-selector">&#9658;</button>
            </div>
        </div>
        <div>
          <h1>Cart</h1>
          <thead>
            <tr>
              <th>Robot</th>
              <th class="cost">Cost</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(robot, idx) in cart" :key="idx">
              <td>{{robot.head.title}}</td>
              <td class="cost">{{robot.cost}}</td>
            </tr>
          </tbody>
        </div>
    </div>
</template>

<script>
import availableParts from '../data/parts';

function getPrevValidIdx(idx, length) {
  const deprecatedIdx = idx - 1;
  return deprecatedIdx < 0 ? length - 1 : deprecatedIdx;
}

function getNextValidIdx(idx, length) {
  const incrmntdIdx = idx + 1;
  return incrmntdIdx > length - 1 ? 0 : incrmntdIdx;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      cart: [],
      selectedHeadIdx: 0,
      selectedLeftArmIdx: 0,
      selectedTorsoIdx: 0,
      selectedRightArmIdx: 0,
      selectedBaseIdx: 0,
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIdx],
        leftArm: availableParts.arms[this.selectedLeftArmIdx],
        torso: availableParts.torsos[this.selectedTorsoIdx],
        rightArm: availableParts.arms[this.selectedRightArmIdx],
        base: availableParts.bases[this.selectedBaseIdx],
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.leftArm.cost + robot.torso.cost
        + robot.rightArm.cost + robot.base.cost;
      this.cart.push({ ...robot, cost });
      console.log(this.cart);
      // this.cart.push(Object.assign({}, robot, { cost }));
    },

    selectNextHead() {
      this.selectedHeadIdx = getNextValidIdx(this.selectedHeadIdx, availableParts.heads.length);
    },

    selectPrevHead() {
      this.selectedHeadIdx = getPrevValidIdx(this.selectedHeadIdx, availableParts.heads.length);
    },

    selectNextLeftArm() {
      this.selectedLeftArmIdx = getNextValidIdx(
        this.selectedLeftArmIdx, availableParts.arms.length,
      );
    },

    selectPrevLeftArm() {
      this.selectedLeftArmIdx = getPrevValidIdx(
        this.selectedLeftArmIdx, availableParts.arms.length,
      );
    },

    selectNextTorso() {
      this.selectedTorsoIdx = getNextValidIdx(this.selectedTorsoIdx, availableParts.torsos.length);
    },

    selectPrevTorso() {
      this.selectedTorsoIdx = getPrevValidIdx(this.selectedTorsoIdx, availableParts.torsos.length);
    },

    selectNextRightArm() {
      this.selectedRightArmIdx = getNextValidIdx(
        this.selectedRightArmIdx, availableParts.arms.length,
      );
    },

    selectPrevRightArm() {
      this.selectedRightArmIdx = getPrevValidIdx(
        this.selectedRightArmIdx, availableParts.arms.length,
      );
    },

    selectNextBase() {
      this.selectedBaseIdx = getNextValidIdx(this.selectedBaseIdx, availableParts.bases.length);
    },

    selectPrevBase() {
      this.selectedBaseIdx = getPrevValidIdx(this.selectedBaseIdx, availableParts.bases.length);
    },
  },
};
</script>

<style scoped lang="less">
.content {
  position: relative;
}
.add-to-cart {
  position: absolute;
  right: 30px;
  width: 220px;
  padding: 3px;
  font-size: 16px;
}
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.robot-head-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.robot-left-arm-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.robot-right-arm-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.robot-torso-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.robot-base-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  color: red;
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
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
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
td, th {
  text-align: left;
  padding: 5px;
  padding-right: 20px;
}
.cost {
  text-align: right;
}
</style>
