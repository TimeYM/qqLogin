<template>
    <div>

        <button @click="qqLogin">qq登录</button>
    </div>
</template>

<script>
    export default {
        name: "home",
        mounted() {
            this.$electron.ipcRenderer.on('reply', (e, data) => {
                console.log(data);
                let httpCode = data.request_code ? data.request_code[0] : '';
                if (httpCode === '1') {
                    alert('登录成功')
                }
            })
        },
        methods: {
            qqLogin() {
                this.$http.get('http://tp5.cn/')
                    .then((result) => {
                        if (result.data.status === 1) {
                            this.$electron.ipcRenderer.send('qqLogin', {url: result.data.data});
                        }
                    })
                    .catch()
            },
        }
    }
</script>
