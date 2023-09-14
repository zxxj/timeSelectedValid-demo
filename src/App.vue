<template>
  <div class="box">
    <a-form
    ref="formRef"
    :model="formState"
    :rules="rules"
    :label-col="labelCol"
    :wrapper-col="wrapperCol"
  >

  <div class="one">
    <a-form-item ref="time1" name="time1">
      <a-time-picker v-model:value="formState.time1" format="HH:mm" style="width: 300px;" @change="time1HandleChange" @openChange="openChange(1)" />
    </a-form-item>

    <a-form-item ref="time1" name="time1End">
      <a-time-picker v-model:value="formState.time1End" format="HH:mm" style="width: 300px;" @change="time1EndHandleChange" />
    </a-form-item>
  </div>

  <div class="one">
    <a-form-item ref="time2" name="time2">
      <a-time-picker v-model:value="formState.time2" format="HH:mm" style="width: 300px;" @change="time2HandleChange" @openChange="openChange(2)" />
    </a-form-item>

    <a-form-item ref="time2" name="time2End">
      <a-time-picker v-model:value="formState.time2End" format="HH:mm" style="width: 300px;" @change="time2EndHandleChange" />
    </a-form-item>
  </div>

  <div class="one">
    <a-form-item ref="time3" name="time3">
      <a-time-picker v-model:value="formState.time3" format="HH:mm" style="width: 300px;" @change="time3HandleChange" @openChange="openChange(3)" />
    </a-form-item>

    <a-form-item ref="time3" name="time3End">
      <a-time-picker v-model:value="formState.time3End" format="HH:mm" style="width: 300px;" @change="time3EndHandleChange" />
    </a-form-item>
  </div>

    <a-form-item :wrapper-col="{ span: 14, offset: 4 }">
      <a-button type="primary" @click="onSubmit">确定</a-button>
    </a-form-item>
  </a-form>
  </div>
</template>
<script setup>
import { reactive, ref, toRaw } from 'vue'; 
import { message } from 'ant-design-vue';

const formRef = ref();
const labelCol = {
  span: 5,
};
const wrapperCol = {
  span: 13,
};
const formState = reactive({});

const timeObj = ref({})

const rules = {
  time1: [
    {
      required: true,
      message: '请输入时间',
      trigger: 'change',
    },
  ],
  time1End: [
    {
      required: true,
      message: '请输入结束时间',
      trigger: 'change',
    },
    
  ],
  time2: [
    {
      required: true,
      message: '请输入时间',
      trigger: 'change',
    },
  ],
  time2End: [
    {
      required: true,
      message: '请输入结束时间',
      trigger: 'change',
    },
    
  ],
  time3: [
    {
      required: true,
      message: '请输入时间',
      trigger: 'change',
    },
  ],
  time3End: [
    {
      required: true,
      message: '请输入结束时间',
      trigger: 'change',
    },
    
  ]
};

const time1HandleChange = (selectTime) => {
  timeObj.value.time1start =  selectTime.$d.getTime()
  if(timeObj.value.time1start && timeObj.value.time1End) {
    if(timeObj.value.time1start >= timeObj.value.time1End) {
      message.error('开始时间不能大于结束时间')
    }
  }
}

const time1EndHandleChange = (selectTime) => {
  timeObj.value.time1End =  selectTime.$d.getTime()
  if(timeObj.value.time1start && timeObj.value.time1End) {
    if(timeObj.value.time1End <=timeObj.value.time1start ) {
      message.error('结束时间不能小于开始时间')
    }
}
}

const time2HandleChange = (selectTime) => {
 const timeArr =  Object.values(timeObj.value)

for (const time of timeArr) {
  if(selectTime <= time) {
    message.error('第二时段的开始时间不能小之前时段')
    return
  }
}
 timeObj.value.time2start =  selectTime.$d.getTime()
}

const time2EndHandleChange = (selectTime) => {
 const timeArr =  Object.values(timeObj.value)
 for (const time of timeArr) {
  if(selectTime <= time) {
    message.error('第二时段的结束时间不能小之前时段')
    return
  }
}
 timeObj.value.time2End =  selectTime.$d.getTime()
}

const time3HandleChange = (selectTime) => {
 const timeArr =  Object.values(timeObj.value)

for (const time of timeArr) {
  if(selectTime <= time) {
    message.error('第三时段的开始时间不能小之前时段')
    return
  }
}
 timeObj.value.time3start =  selectTime.$d.getTime()
}

const time3EndHandleChange = (selectTime) => {
 const timeArr =  Object.values(timeObj.value)
 for (const time of timeArr) {
  if(selectTime <= time) {
    message.error('第三时段的结束时间不能小之前时段')
    return
  }
}
 timeObj.value.time3End =  selectTime.$d.getTime()
}

const openChange = (openKey) => {
  switch(openKey) {
    case 1: 
      formState.time1End = ''
      timeObj.value.time1End = ''
      break
      case 2:
      formState.time2End = ''
      timeObj.value.time2End = ''
      break
      case 3:
      formState.time3End = ''
      timeObj.value.time3End = ''
      break
  }
}
const onSubmit = () => {
  formRef.value
    .validate()
    .then(() => {
      console.log('values', formState, toRaw(formState));
    })
    .catch(error => {
      console.log('error', error);
    });
};
</script>

<style>
.box {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.one {
  display: flex;
}
</style>