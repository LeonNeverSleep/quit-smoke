<script setup lang="ts">
import { ref, computed } from "vue";
import Langs from "./components/Langs.vue";
const smokeYear = ref(0);
const smokeDaily = ref(0);
const averagePrice = ref(0);
const total = computed(() => smokeYear.value * 365 * smokeDaily.value);
const cost = computed(() => total.value * (averagePrice.value / 20));
const costAccessList = [
  // 0-1000元，每500元划分一档
  {
    between: [0, 70],
    donate: "几顶迷彩帽",
    displacement: "面包瓜子矿泉水",
  },
  {
    between: [71, 210],
    donate: "一两盒子弹",
    displacement: "一次便饭",
  },
  {
    between: [211, 500],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [501, 1000],
    donate: "一副战斗防风镜",
    displacement: "一箱油钱",
  },
  {
    between: [1001, 1500],
    donate: "一个战斗头盔",
    displacement: "省内短途一日游",
  },
  {
    between: [1501, 2500],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [2501, 5000],
    donate: "一把92式自动手枪",
    displacement: "一只apple watch",
  },
  {
    between: [5001, 7500],
    donate: "一支95式步枪",
    displacement: "一部iPhone",
  },
  {
    between: [7501, 10000],
    donate: "一部HGJ激光测距仪",
    displacement: "一次家庭聚餐",
  },
  {
    between: [10001, 15000],
    donate: "82式夜视仪",
    displacement: "台式机+2K显示器",
  },
  {
    between: [15001, 20000],
    donate: "TBR-115式电台",
    displacement: "一个LV的包包",
  },
  {
    between: [20001, 25000],
    donate: "一部军用对讲机",
    displacement: "一次家庭聚餐",
  },
  {
    between: [25001, 50000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [50001, 75000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [75001, 100000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [100001, 150000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [150001, 200000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [200001, 500000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
  {
    between: [500001, 1000000],
    donate: "一双军用战斗靴",
    displacement: "一次家庭聚餐",
  },
];
const totalAccessList = [
  {
    between: [1, 3],
    advice: "搁这养生呢？不行憋抽了咱戒了",
  },
  {
    between: [4, 10],
    advice: "还行,保持这个节奏~",
  },
  {
    between: [11, 15],
    advice: "得为健康考虑一下了,先从一天5根的目标开始慢慢戒",
  },
  {
    between: [16, 20],
    advice: "可以先试试一天半包,后面习惯了再慢慢减少一天抽的量",
  },
  {
    between: [21, 30],
    advice: "不是哥们儿你烟囱啊,再抽这么猛要噶了!赶紧开始戒烟",
  },
  {
    between: [31, 50],
    advice: "哥们儿你吹牛逼呢,一天两包抽完人还在吗？能救你的只有你自己了！",
  },
  {
    between: [51, 10000],
    advice: "别闹！",
  },
];
const findAdviceBySmokeDaily = computed(() => {
  let advice = "";
  totalAccessList.forEach((item) => {
    if (
      smokeDaily.value >= item.between[0] &&
      smokeDaily.value <= item.between[1]
    ) {
      advice = item.advice;
    }
  });
  return advice;
});
const findDonateByCost = computed(() => {
  let donate = "";
  costAccessList.forEach((item) => {
    if (cost.value >= item.between[0] && cost.value <= item.between[1]) {
      donate = item.donate;
    }
  });
  return donate;
});
const findDisplacementByCost = computed(() => {
  let displacement = "";
  costAccessList.forEach((item) => {
    if (cost.value >= item.between[0] && cost.value <= item.between[1]) {
      displacement = item.displacement;
    }
  });
  return displacement;
});
const handleSmokeDailyChange = (value: number) => {
  smokeDaily.value = value;
};
</script>

<template>
  <div class="home-container">
    <h1>您该戒烟了！</h1>
    <h1 style="color: #e60012">未成年禁止吸烟!</h1>
    <el-form
      style="
        min-width: 500px;
        display: flex;
        justify-content: space-around;
        align-items: center;
        flex-direction: column;
      "
    >
      <el-form-item label="您的烟龄(年)">
        <el-input-number v-model="smokeYear" :min="0" :max="50" />
      </el-form-item>
      <el-form-item label="一天的量(根)">
        <el-input-number
          v-model="smokeDaily"
          @change="handleSmokeDailyChange"
          :min="1"
          :max="100"
        />
      </el-form-item>
      <el-form-item label="烟均价(元/包)">
        <el-input-number v-model="averagePrice" :min="10" :max="200" />
      </el-form-item>
    </el-form>
    <Langs />
    <el-card style="min-width: 700px">
      <div class="weapon-item">
        <h3>您大约已经吸了:</h3>
        <h4>{{ total }}根</h4>
      </div>
      <div class="weapon-item">
        <h3>累计大约花费:</h3>
        <h4>{{ cost }}元</h4>
      </div>
      <div class="weapon-item">
        <h3>军备贡献量:</h3>
        <h4>{{ findDonateByCost }}</h4>
      </div>
      <div class="weapon-item">
        <h3>不抽烟省下来的钱可以置换:</h3>
        <h4>{{ findDisplacementByCost }}</h4>
      </div>
      <template #footer>
        <div class="weapon-item2">
          <h3>戒烟建议:</h3>
          <h4>{{ findAdviceBySmokeDaily }}</h4>
        </div>
      </template>
    </el-card>
  </div>
</template>

<style scoped>
.home-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
}
h1 {
  margin-bottom: 50px;
}
.weapon-item {
  width: 95%;
  height: 50px;
  padding-left: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.weapon-item2 {
  width: 95%;
  height: 100px;
  padding-left: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
