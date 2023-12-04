<template>
    <div class="bg">
        <div class="img-box">
            <img width="100" src="../assets/image/game.png">
        </div>
        <div class="btn" @click="router.back()">Return</div>
        <p class="ww">What is the Process of Learning? Drag and order.</p>
        <div class="buttons-container">
            <div v-for="(button, index) in buttons" :key="index" style="width: 100%; display: flex;align-items: center;">
                <div class="button" draggable="true" @dragstart="onDragStart(index)" @dragover.prevent="onDragOver"
                    @drop="onDrop(index)">
                    <span style="color: red;">{{ button.charAt(0) }}</span>{{ button.slice(1) }}
                </div>
                <div class="arrow" v-if="index !== 3">&#8594;</div>
            </div>

        </div>
        <div v-if="isOrderCorrect" class="success-message">Congrats! Now you know the process!</div>
        <div v-else class="failure-message">Opps! That is not the right process!</div>
    </div>
</template>
  
<script>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router'
const shuffleArray = (array) => {
    let currentIndex = array.length;
    let randomIndex;

    while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
    }

    return array;
};

export default {
    setup() {
        const router = useRouter()
        const correctOrder = ['Design', 'Build', 'Test', 'Learn'];
        const shuffledOrder = shuffleArray([...correctOrder]);

        const buttons = ref(shuffledOrder);
        const isOrderCorrect = ref(false);
        const draggedIndex = ref(null);

        const onDragStart = (index) => {
            draggedIndex.value = index;
        };

        const onDragOver = (event) => {
            event.dataTransfer.dropEffect = 'move';
        };

        const onDrop = (index) => {
            const draggedButton = buttons.value[draggedIndex.value];
            buttons.value[draggedIndex.value] = buttons.value[index];
            buttons.value[index] = draggedButton;
            draggedIndex.value = null;
            checkOrder();
        };

        const checkOrder = () => {
            isOrderCorrect.value = JSON.stringify(buttons.value) === JSON.stringify(correctOrder);
        };

        onMounted(() => {
            checkOrder();
        });

        return {
            buttons,
            isOrderCorrect,
            onDragStart,
            onDragOver,
            onDrop,
            checkOrder,
            router
        };
    },
};
</script>
  
<style>
.bg {
    height: 100%;
    padding: 0px 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-position: center center;
    background-repeat: no-repeat;
    background: url('../assets/image/bg.jpg');
    background-size: 100% cover;
}

.buttons-container {
    width: 100%;
    justify-content: center;
    display: flex;
}
.btn {
    width: 80px;
    height: 30px;
    line-height: 30px;
    padding: 0 10px;
    margin: 20px auto;
    font-size: 14px;
    border: 1px solid #ffffffdd;
    border-radius: 15px;
    cursor: pointer;
    color: #FFF;
    text-align: center;
  }
.button {
    color: #FFF;
    height: 200px;
    border: 1px solid #ccc;
    margin: 5px;
    display: flex;
    font-weight: bold;
    font-size: 24px;
    justify-content: center;
    align-items: center;
    cursor: grab;
    width: 100%;
}

.success-message,
.failure-message {
    margin-top: 30px;
    font-weight: bold;
    font-size: 28px;
    text-align: center;
}

.success-message {
    color: green;
}

.ww {
    text-align: center;
    color: rgb(0, 200, 255);
    font-size: 40px;
}

.arrow {
    color: white;
    font-size: 30px;
    margin: 0 10px;
}

.failure-message {
    color: red;
}
</style>
  