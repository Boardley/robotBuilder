<template>
  <div class="content">
    <div class="preview">
      <CollapsibleSection>
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
      </CollapsibleSection>
      <button @click="addToCart()" class="add-to-cart">Add To Cart</button>
    </div>

    <div class="top-row">
        <!-- <div class="robot-name">
          {{selectedRobot.head.title}}
           <span v-if="selectedRobot.head.onSale" class="sale">Sale</span>
        </div>
        /.robot-name -->
      <PartSelector
        :parts="availableParts.heads"
        position="top"
        @partSelected="part => selectedRobot.head = part"
      />
    </div>
    <div class="middle-row">
      <PartSelector
        :parts="availableParts.arms"
        position="left"
        @partSelected="part => selectedRobot.leftArm = part"
      />
      <PartSelector
        :parts="availableParts.torsos"
        position="center"
        @partSelected="part => selectedRobot.torso = part"
      />
      <PartSelector
        :parts="availableParts.arms"
        position="right"
        @partSelected="part => selectedRobot.rightArm = part"
      />
    </div>
    <div class="bottom-row">
      <PartSelector
        :parts="availableParts.bases"
        position="bottom"
        @partSelected="part => selectedRobot.base = part"
      />
    </div>
    <div>
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in myCart" :key="index">
            <td>{{robot.head.title}}</td>
            <td class="cost">{{robot.cost}}</td>
          </tr>
          <tr><td colspan="2" class="cost"><strong>Total:</strong> ${{cartTotal.toFixed(2)}}</td></tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import availableParts from "../../data/parts";
import PartSelector from "./PartSelector.vue";
import CollapsibleSection from "../shared/CollapsibleSection.vue";

export default {
  name: "RobotBuilder",
  beforeRouteLeave(tp,from, next) {
    if(this.addedToCart) {
      next(true);
    } else {
      const response = confirm('You have not added your robot to your cart, are you sure you want to leave?');
      next(response);
    }
  },
  components: {
    CollapsibleSection,
    PartSelector
  },
  data() {
    return {
      availableParts,
      addedToCart: false,
      cartTotal: 0,
      myCart: [],
      selectedRobot: {
        base: {},
        head: {},
        leftArm: {},
        rightArm: {},
        torso: {}
      }
    };
  },
  computed: {},
  mounted() {
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost =
        robot.head.cost +
        robot.leftArm.cost +
        robot.rightArm.cost +
        robot.torso.cost +
        robot.base.cost;
      this.myCart.push(Object.assign({}, robot, { cost }));
      this.cartTotal += cost;
    }
  }
};
</script>

<style lang="scss">
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;

  img {
    width: 165px;
  }
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
.next-selector,
.prev-selector {
  height: 171px;
  position: absolute;
  top: -3px;
  width: 25px;
  z-index: 1;
}

.prev-selector {
  left: -28px;
}

.next-selector {
  right: -28px;
}

.left,
.right {
  .next-selector,
  .prev-selector {
    height: 25px;
    width: 144px;
  }
}

.left {
  border-right: none;

  img {
    transform: rotate(-90deg);
  }

  .prev-selector {
    top: -28px;
    left: -3px;
  }
  .next-selector {
    top: auto;
    bottom: -28px;
    left: -3px;
  }
}
.right {
  border-left: none;

  img {
    transform: rotate(90deg);
  }

  .next-selector,
  .prev-selector {
    left: 24px;
  }

  .prev-selector {
    top: -28px;
  }
  .next-selector {
    top: auto;
    bottom: -28px;
  }
  .next-selector {
    right: -3px;
  }
}

.bottom {
  border-top: none;
}

.center {
  .prev-selector,
  .next-selector {
    opacity: 0.8;
  }
}

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.sale {
  color: red;
}
.add-to-cart {
  font-size: 16px;
  padding: 5px 50px;
  width: 100%;
}
.content {
  position: relative;
}
td,
th {
  padding: 5px;
  padding-right: 20px;
  text-align: left;

  &.cost {
    text-align: right;
  }
}

// Robot Preview
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
</style>
