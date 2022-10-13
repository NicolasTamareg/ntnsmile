<script>
export default {

    data() {
            return {
                newTask: "",
                taskList: [],
            };
        },
        methods: {
            addTask: function () {
                if (this.newTask === "") {
                    return;
                }
                const newTask = {
                    text: this.newTask,
                    status: "todo",
                };
                this.taskList.push(newTask);
                this.newTask = "";
            }
        },
}
</script>


<template>
    <div class="main-profil">
        <div class="fond-ecran">
            <img class="main-image" src="https://www.coursinfo.fr/wp-content/uploads/2016/04/facebook-logo.jpg" alt="">
        </div>
        <div class="photo-pseudo">
            <img class="img-profil" src="https://picsum.photos/seed/picsum/200/200" alt="">
            <h2>Pierre Richard</h2>
        </div>
        <div class="mini-titre">
        </div>
        <ul>
        </ul>
    </div>
</template>

<style>
.main-profil{
    margin: auto;
    justify-content: center;
    height: 100%;
    width: 80%;
}

.photo-pseudo{
    display: flex;
    align-items: flex-end;
    margin-left: 10%;
    transform: translateY(-60%);
}

ul{
    text-align: center;
}
.img-profil{
    display: flex;
    flex-direction: column;
    border-radius: 50%;
}


.mini-titre{
    text-align: center;
}
</style>