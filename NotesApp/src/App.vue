<template>
    <main>
        <div v-if="isShowed" class="overlay">
            <div class="modal">
                <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
                <p v-if="this.errorMessage"> {{ this.errorMessage }}</p>
                <button @click="addNote()">Add Note</button>
                <button class="close" @click="isShowed=False">Close</button>
            </div>
        </div>
        <div class="container">
            <header>
                <h1>Notes</h1>
                <button @click="isShowed=true">+</button>
            </header>

            <div class="cards-container">
                <!-- note in :style.-->
                <!-- if we use only style, style will considered as plain text-->
                <!-- but if added :, style will be considered as javascript-->

                <!-- :key is a unique key used by vue to identify div object-->
                <!-- when update or delete.-->
                <!-- rather than delete all and render from beginning all elements through loop-->
                <!-- !!! TYPE expect :key="note.id" but written down :key="no[d]e.id"-->
                <div v-for="note in notes"
                     class="card"
                     :key="note.id"
                     :style="{backgroundColor:note.backgroundColor}"
                >
                    {{ note.id }}
                    <p class="main-text">{{ note.text }}</p>
                    <p class="date ">{{ note.date.toLocaleDateString("en-US") }}</p>
                </div>

            </div>
        </div>
    </main>
</template>

<script>
export default ({
    data() {
        return {
            isShowed: false,
            newNote: "",
            notes: [],
            errorMessage: ""
        }
    },
    methods: {
        addNote() {
            if (this.newNote.length < 10) {
                return this.errorMessage = "Minimum 10 character length!!"
            }

            this.notes.push({
                id: Math.floor(Math.random() * 1000000),
                text: this.newNote,
                date: new Date(),
                backgroundColor: this.getRandomColor()
            })

            this.newNote = "";
            this.isShowed = false;
            this.errorMessage = ""
        },

        getRandomColor() {
            return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
        }
    }
})

</script>

<style scoped>
main {
    height: 100vh;
    width: 100vw;
}

.container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
}

header button {
    border: None;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: gray;
    border-radius: 100%;
    color: white;
    font-size: 20px;
}

.card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 187, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    font-size: 25px;

}

.date {
    font-size: 12.5px;
    font-weight: bold;
}

.cards-container {
    display: flex;
    flex-wrap: wrap;
}

.overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;

}

.modal textarea {
    font-size: 20px;
}

.modal button {
    padding: 10px 20px;
    font-size: 25px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
}

.modal .close {
    background-color: rgb(192, 15, 15);
    margin-top: 7px;
}

.modal p {
    color: rgb(192, 15, 15);
}
</style>
