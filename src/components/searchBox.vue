<template>
    <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Where" 
        autofocus 
        v-model="queryValue"
        @keypress="queryGetter"
        />
        <span 
        class="value-deletion" 
        v-if="queryValue != ''"
        @click="deleteQueryValue()">&#10006;</span>
    </div>
</template>

<script>
export default {
    name: 'searchBox',
    data () {
        return {
            queryGetterFlag: true,
            queryValue: ''
        }
    },
    methods: {
        queryGetter (e) {
            if (e.key == 'Enter' && this.queryGetterFlag == true) {
                // カスタムイベントplaceを登録し、placeが発火するとfetchWeatherを実行
                this.$emit('place', this.queryValue)
                this.queryGetterFlag = false;
                
                //ダブルクリック（タップ）防止。2秒後にqueryGetterを再度実行可能状態に戻す
                setTimeout(() => {
                this.queryGetterFlag = true
            }, 2000)
            }
        },
        deleteQueryValue() {
            // クリックするとqueryValueを空にする
            this.queryValue = ''
        }
    }
}

</script>

<style>
.search-box {
    position: relative;
    margin-top: 20px;
    width: 100%;
}

.search-box .value-deletion {
    font-size: 18px;
    color: #313131;
    position: absolute;
    top: 50%;
    right: 5px;
    transform: translate(-50%, -50%);
}

.search-box .search-bar {
    width: 100%;
    padding: 15px;
    color: #313131;
    font-size: 21px;
    appearance: none;
    -webkit-appearance: none;
    border: none;
    outline: none;
    background: none;
    background-color: rgba(255, 255, 255, 0.75);
    box-shadow: 0 0 8px rgba(0, 0, 0, .2);
}

.search-box .search-bar:focus {
    box-shadow: 0 0 16px rgba(0, 0, 0, .2);
    background-color: rgba(255, 255, 255, .9);
}
</style>