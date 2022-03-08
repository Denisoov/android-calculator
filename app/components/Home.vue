<template>
  <Page class="page">
    <ActionBar class="action-bar" title="Calculator"> </ActionBar>

    <StackLayout class="wrapper-calculator">
      <Label class="operations" :text="result" />
      <Label class="result" :text="result" />
      <FlexboxLayout flexDirection="row">
        <FlexboxLayout class="wrapper-left">
          <!-- Дополнительно -->
          <FlexboxLayout class="wrapper-left__additionals">
            <ButtonNumber :buttonValue="'c'" />
            <ButtonNumber :buttonValue="'^'" />
          </FlexboxLayout>

          <!-- Цифры -->
          <FlexboxLayout class="numbers">
            <ButtonNumber
              v-for="number in 9"
              :key="number"
              :buttonValue="number"
            />

            <ButtonNumber :buttonValue="'0'" />
            <ButtonNumber :buttonValue="'.'" />
            <ButtonNumber :buttonValue="'='" />
          </FlexboxLayout>
        </FlexboxLayout>

        <!-- Действия -->
        <FlexboxLayout class="wrapper-right-actions">
          <ButtonNumber
            v-for="(action, idx) in actions"
            :key="idx"
            :buttonValue="action"
          />
        </FlexboxLayout>
      </FlexboxLayout>
    </StackLayout>
  </Page>
</template>

<script>
import ButtonNumber from "@/components/ButtonNumber.vue";

export default {
  components: {
    ButtonNumber,
  },
  data() {
    return {
      result: 0,
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      actions: ["÷", "×", "-", "+"],
    };
  },
};
</script>

<style lang="scss" scoped>
.wrapper-left {
  width: 75%;
  height: 100%;
  flex-wrap: wrap;

  &__additionals {
    height: auto;

    Button {
      width: 50%;
      background-color: #ff9f0b;

      &:active {
        background-color: rgb(155, 91, 7);
      }
    }
  }
}
.wrapper-right-actions {
  width: 25%;
  height: 100%;
  flex-direction: column;

  Button {
    height: 25%;
    background-color: #ff9f0b;

    &:active {
      background-color: rgb(155, 91, 7);
    }
  }
}
Button {
  margin: 0;
  font-size: 26;
  border-radius: 1%;
  color: #333;
}
Label {
  font-size: 32;
  text-align: right;
  background-color: rgb(255, 221, 129);
  color: #111;
  padding: 20;
}
.result {
  font-size: 29;
  color: #aaa;
}

.numbers {
  flex-wrap: wrap;
  width: 100%;

  Button {
    width: 33.33%;
    height: 20%;

    &:active {
      background-color: #aaa;
    }
  }
}
</style>
