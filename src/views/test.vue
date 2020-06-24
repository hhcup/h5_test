<template>
    <div class="test">
        <h1>hello world</h1>
        <h3>image图片 - 前置摄像头调用</h3>
        <input id="upimg" @change="con()" type="file" accept="image/*" capture="user">
        <img class="imgg" src="" alt="">
    </div>
</template>

<script>
    import EXIF from "exif-js"
    export default {
        name: "test",
        data(){
            return{
                imgs:"",
                imgsrc:''
            }
        },
        created() {
        },
        methods:{
            con(){
                let imgEl = document.querySelector("#upimg");
                let imgg = document.querySelector(".imgg");
                this.imgsrc = imgEl.files[0];
                var reader = new FileReader();
                reader.addEventListener("load", function () {
                    imgg.src = reader.result;
                    EXIF.getData(imgg, function() {
                        EXIF.getAllTags(this);
                        let Orientation = EXIF.getTag(this, 'Orientation');
                        alert(Orientation,"###");
                    });
                }, false);
                reader.readAsDataURL(imgEl.files[0]);
            }
        },
    }
</script>

<style scoped>
.imgg{
    max-width: 100%;
}
</style>