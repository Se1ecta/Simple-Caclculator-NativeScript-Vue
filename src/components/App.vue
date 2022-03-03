<template>
  <Page>
    <ActionBar title="Calculator" />
    <StackLayout class="calculator">
      <FlexboxLayout
        class="base-input"
        borderRadius="15"
        width="100%"
        height="25%"
        flexDirection="column"
      >
        <Label
          :text="previousValue"
          fontSize="16"
          justifyContent="flex-end"
          alignSelf="flex-end"
          marginRight="20"
        ></Label>
        <Label
          class="base-input-value"
          alignSelf="flex-end"
          :text="currentValue"
          marginRight="20"
        ></Label>
      </FlexboxLayout>
      <StackLayout class="buttons-body">
        <StackLayout
          class="buttons-container"
          orientation="horizontal"
          paddingLeft="0"
        >
          <Button class="buttons" text="C" @tap="clean()"></Button>
          <Button class="buttons" text="+/-"></Button>
          <Button class="buttons" text="%"></Button>
          <Button class="buttons" text="DEL" @tap="deleteButton()"></Button>
        </StackLayout>
        <StackLayout class="buttons-container" orientation="horizontal">
          <Button class="buttons" text="9" @tap="insertValue('9')"></Button>
          <Button class="buttons" text="8" @tap="insertValue('8')"></Button>
          <Button class="buttons" text="7" @tap="insertValue('7')"></Button>
          <Button
            class="buttons operator"
            text="/"
            @tap="insertValue('/')"
          ></Button>
        </StackLayout>
        <StackLayout class="buttons-container" orientation="horizontal">
          <Button class="buttons" text="6" @tap="insertValue('6')"></Button>
          <Button class="buttons" text="5" @tap="insertValue('5')"></Button>
          <Button class="buttons" text="4" @tap="insertValue('4')"></Button>
          <Button
            class="buttons operator"
            text="*"
            @tap="insertValue('*')"
          ></Button>
        </StackLayout>
        <StackLayout class="buttons-container" orientation="horizontal">
          <Button class="buttons" text="3" @tap="insertValue('3')"></Button>
          <Button class="buttons" text="2" @tap="insertValue('2')"></Button>
          <Button class="buttons" text="1" @tap="insertValue('1')"></Button>
          <Button
            class="buttons operator"
            text="-"
            @tap="insertValue('-')"
          ></Button>
        </StackLayout>
        <StackLayout class="buttons-container" orientation="horizontal">
          <Button class="buttons" text="0" @tap="insertValue('0')"></Button>
          <Button class="buttons" text="." @tap="insertValue('.')"></Button>
          <Button class="buttons equal" text="=" @tap="equal()"></Button>
          <Button
            class="buttons operator"
            text="+"
            @tap="insertValue('+')"
          ></Button>
        </StackLayout>
      </StackLayout>
    </StackLayout>
  </Page>
</template>

<script>
export default {
  data() {
    return {
      previousValue: "",
      currentValue: "",
      operator: null,
    };
  },
  methods: {
    insertValue(value) {
      this.currentValue = this.currentValue + "" + value;
    },
    setOperator(op) {
      if (this.operator != null) {
        this.equal();
      }
      this.operator = op;
      this.previousValue = this.currentValue;
      this.currentValue = "";
    },
    deleteButton() {
      this.currentValue = this.currentValue.toString().slice(0, -1);
    },
    clean() {
      this.currentValue = "";
      this.previousValue = "";
    },
    equal() {
      this.previousValue = this.currentValue;
      this.currentValue = eval(this.currentValue);
    },
  },
};
</script>

<style scoped lang="scss">
ActionBar {
  color: #000000;
  text-align: center;
}

.calculator {
  padding: 15 5;
  .base-input {
    display: flex;
    justify-content: flex-end;
    background: #8a2be2;
    &-value {
      color: white;
      font-size: 40;
    }
  }
  .buttons-body {
    width: 100%;
    padding: 0 auto;
    margin: 0 auto;
    .buttons-container {
      margin: 0;
      .buttons {
        width: 70;
        height: 70;
        margin: 0 0 0 12;
        font-size: 20;
        &.equal {
          background: orange;
          color: white;
        }
        &.operator {
          background: rgb(250, 250, 250);
          color: orange;
        }
      }
    }
  }
}

.button {
  width: 75;
  height: 75;
}
</style>
