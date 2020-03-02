<template>
    <div class="comment-box" v-if="typeof weather.main != 'undefined'">
        <div class="icon-box">
            <img :src="setImg">
        </div>
        <p class="comment">The current weather in <span class="font-stressed">{{ weather.name }}</span> is "{{ weather.weather[0].main}}". {{ weatherComment() }} </p>
    </div>
</template>

<script>

export default {
    props: ['weather', 'weatherImgUrl'],
    name: 'commentBox',
    computed: {
        setImg() {
            // 結果として渡された天気の情報をpathを考慮して'.'を追加
            return '.' + this.weatherImgUrl
        }
    },
    methods: {
        weatherComment() {
            // commentObj内の配列からコメントを抽出するindexとして用いる
            let randomNumber = Math.floor(Math.random() * 3);

            const commentObj = {
                // Clear時に表示するコメント
                fine: ["Yes! Let's barbecue outside right now!", 
                        "You are so lucky today! Why don't you ask out someone special?", 
                        "There is no choice but to go outside right now!"
                ],
                // Rain,Drizzle, Snow時に表示するコメント
                bad: ["You better to stay at home today. Otherwise, you'll catch a cold.", 
                        "I hope it'll be fine tomorrow.", 
                        "All you have to do is stay at home."
                ],
                // Fog, Mist, Haze時に表示するコメント
                notBad: ["Not bad.", 
                        "It'd be fine. I guess.", 
                        "I don't know whether it'll be fine or not..."]
            }
            switch(this.weather.weather[0].main) {
                case 'Clear':
                    return commentObj.fine[randomNumber];
                case 'Rain':
                case 'Drizzle':
                case 'Snow':
                    return commentObj.bad[randomNumber];
                case 'Clouds':
                case 'Fog':
                case 'Mist':
                case 'Haze':
                    return commentObj.notBad[randomNumber];
            }
        }
    }
}

</script>

<style>

.font-stressed {
    font-size: 18px;
    font-weight: 700;
}

.comment-box {
    background-color: #FFF;
    border-radius: 10px;
    box-shadow: 0 0 8px rgba(0, 0, 0, .75);
    display: flex;
    align-items: center;
    margin-top: 20px;
    width: 100%;
}

.icon-box {
    border-right: 3px solid #313131;
    padding: 10px;
    width: 30%;
}

.icon-box img {
    width: 100%;
    height: auto;
}

.comment {
    display: inline-block;
    padding: 20px;
    width: 70%;
}
</style>