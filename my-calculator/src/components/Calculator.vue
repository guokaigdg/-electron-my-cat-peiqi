<template>
    <div class="root">
        <div class="top">
            {{ result }}
        </div>
        <div class="button-root">
            <span
                class="button" 
                v-for="item in numList"
                :key="item"
                :class="{'zero-button': item === 0, 'num-buttom': this.numButton.includes(item), 'computer-buttom': this.computerColor.includes(item) }"
                @click="handleClickButton(item)"
            >
               {{ item }}
            </span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Calculator',
    props: {
        msg: {
            type: String,
            default: '计算器',
            required:false
        }
    },
    data() {
        return {
            one: 0, // 第一个数字
            two: 0, // 第二个数字
            operator: null, // 计算符号
            result: 0, /// 计算结果
            numList: ["C", "+/-", "%",  "÷", 7, 8, 9, 'x', 4, 5, 6, '-', 1, 2, 3, "+", 0, '.', '='], // 所有操作符列表
            computer: ["C", "+/-", "%",  "÷", 'x', '-', "+", '.', '='], //计算符号
            computerColor: ["÷", 'x', '-', "+", '.', '='], //  计算区配色Color
            numButton: [7, 8, 9, 4, 5, 6, 1, 2, 3, 0], // 数字区
        }
    },
    methods: {
        handleClickButton(item){
            console.log(`${this.one} ${this.operator} ${this.two} = ${this.result}`);
            // 清空结果
            if(item === 'C'){
                 this.result = 0;
                 this.one = null;
                 this.two = null;
                 this.operator = null;
                 return
            }
            // 计算结果
            if(item === '='){
                if(this.operator === '+'){
                    this.result = Math.floor((this.one + this.two) * 100) / 100;
                }
                if(this.operator === '-'){
                    this.result = Math.floor((this.one - this.two) * 100) / 100;
                }
                if(this.operator === 'x'){
                    this.result = Math.floor((this.one * this.two) * 100) / 100;
                }
                if(this.operator === '÷'){
                    this.result = this.two === 0 ? 0 : Math.floor((this.one / this.two) * 100) / 100;
                }
                this.one = this.result;
            }
            // 最多算8位数字
            if(this.result.toString().length > 8){
                return
            }
            // 输入数字
            if(this.numButton.includes(item)) {
                // 输入第一个数字
                if(!this.operator){
                    //之前输入过数字
                    if(this.one !== null){
                        // 小数处理
                        if(this.one && this.one.indexOf('.')) {
                            this.one = Number(this.one + item);
                        }else{
                            this.one = this.one * 10 + item;
                        }
                    }else{
                        this.one = item;
                    }
                    this.result = this.one;
                    return 
                }
                // 输入第二个数字
                if(this.two !== null){
                    // 小数处理
                    console.log('94----->', this.two);
                    if(this.two && this.two.indexOf('.')) {
                        this.two = Number(this.two + item);
                    }else{
                        this.two = this.two * 10 + item;
                    }
                }else{
                    this.two = item;
                }
                this.result = this.two;
            }
            // 计算符号
            if(this.computer.includes(item)) {
                if(item === '='){
                    return
                }
                if(item === '%'){
                    this.one = this.one === 0 ? 0 : Math.floor((this.one) * 100) / 10000;
                    this.one = Number(this.one);
                    this.result = this.one;
                    
                } else if(item === '+/-'){
                    this.one = -this.one ;
                    this.one = Number(this.one);
                    this.result = this.one;
                } 
                // else if(item === '.'){
                //     // one已经是小数了
                //     if(this.one && this.one.indexOf('.')){
                //         console.log('121------>', this.one);
                //         this.two = this.two.toString() + '.';
                //         this.result = this.two;
                //     }else{
                //         this.one = this.one.toString() + '.';
                //         this.result = this.one;
                //     }
                // }
                else{
                    this.operator = item;
                    this.two = 0;
                }
            }
        }
    }
}
</script>


<style scoped>
.root{
    background:rgb(1, 0, 0);
    height: 812px;
    width: 375px;
    color: rgb(255, 255, 255);
    padding: 5px;
    box-sizing: border-box;
    font-weight: 800;
    
}
.top {
    display: flex;
    flex-direction: column-reverse;
    align-items: flex-end;
    box-sizing: border-box;
    font-size: 50px;
    font-weight: 350;
    width: 100%;
    height: 280px;
    padding-right: 20px;
    padding-bottom: 10px;
}
.button-root {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    flex-wrap: wrap;
    font-size: 30px;
    width: 100%;
}
.button{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80px;
    height: 80px;
    margin-bottom: 15px;
    border-radius: 50%;
    background: rgb(165, 165, 165);
}
.button:active{
    opacity: 0.7;
}
.zero-button{
    width: 170px;
    border-radius: 40px;
}
.num-buttom{
    background: rgb(51, 51, 51);
    opacity: 0.6;
}
.computer-buttom{
    background: rgb(255, 157, 45);
}

</style>
