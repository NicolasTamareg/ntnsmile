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
        <div class="photo-pseudo">
            <img src="https://picsum.photos/seed/picsum/200/200" alt="">
            <h2>Pierre Richard</h2>
        </div>
        <div class="mini-titre">
            <h4>Bienvenue sur votre page de profil</h4>
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
    border: 2px solid black;
}

.photo-pseudo{
    display: flex;
    align-items: flex-end;
    margin-left: 10%;
    border: 2px solid blue;
}

ul{
    text-align: center;
}
img{
    display: flex;
    flex-direction: column;
    border-radius: 50%;
}

.mini-titre{
    text-align: center;
}
</style>