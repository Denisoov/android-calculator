<template>
  <Page class="page">
    <ActionBar class="action-bar" title="Calculator"> </ActionBar>

    <StackLayout class="wrapper-calculator">
      <Label class="operations" :text="enterValues" />
      <Label class="result" :text="result" />
      <FlexboxLayout flexDirection="row">
        <FlexboxLayout class="wrapper-left">
          <!-- Дополнительно -->
          <FlexboxLayout class="wrapper-left__additionals">
            <ButtonNumber @fnEnter="clearCollection" :buttonValue="'c'" />
            <ButtonNumber @fnEnter="collectionEnterOperator" :buttonValue="'^'" />
          </FlexboxLayout>

          <!-- Цифры -->
          <FlexboxLayout class="numbers">
            <ButtonNumber
              @fnEnter="collectionEnterValue"
              v-for="number in 9"
              :key="number"
              :buttonValue="number"
            />
            <ButtonNumber @fnEnter="collectionEnterValue" :buttonValue="'0'" />
            <ButtonNumber @fnEnter="addDot" :buttonValue="'.'" />
            <ButtonNumber @fnEnter="calculation" :buttonValue="'='" />
          </FlexboxLayout>
        </FlexboxLayout>

        <!-- Действия -->
        <FlexboxLayout class="wrapper-right-actions">
          <ButtonNumber
            @fnEnter="collectionEnterOperator"
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
      enterValues: '0',
      actions: ["/", "*", "-", "+"],
    };
  },
  methods: {
    checkDoubleKey(key) {
      const res = this.enterValues
      const lastSymbol = res.length !== 0 ? res[res.length - 1]  : null

      return lastSymbol == key
    },
    checkOperation(key) {
      const operators = ["/", "*", "-", "+", ".", "^"]
      const checkSymbol = operators.includes(key)

      return checkSymbol
    },
    collectionEnterValue(key) {
      this.enterValues == '0' ? this.enterValues = key : this.enterValues += key
    },
    addDot() {
      if (this.enterValues.length !== 0) {
        if (!this.checkOperation(this.enterValues[this.enterValues.length - 1])) 
          this.enterValues += '.'
      }
      else {
        if (this.enterValues.substr(this.enterValues.length - 2, 2) !== '.') {
          this.enterValues += '.'
        }
      }
    },
    collectionEnterOperator(key) {  
      if (this.enterValues.length !== 1) {
        this.checkOperation(this.enterValues[this.enterValues.length - 1]) 
          ? this.enterValues = this.enterValues.replace(/.$/gi, String(key)) 
          : this.collectionEnterValue(key)
      }
    },
    clearCollection() {
      this.enterValues !== '0' 
          ? this.enterValues = '0'
          : this.result = 0 
    },
    calculation() {
      const values = this.enterValues.replace(/\^/g, "**" )

      try {
        const res = eval(values)

        if (res == 'Infinity') {
          this.enterValues = '0'
          this.result = 'Ошибка!'
        } else {
          this.result = eval(values)
        }

      } catch (err) {
        this.enterValues = '0'
        this.result = 'Ошибка!'
      }
    }
  }
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
