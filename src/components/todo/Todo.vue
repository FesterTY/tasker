<template>
    <div id='todo'>
        <div id='todoComponents'>
            <div>
                <h2 class='header'>TODO LIST</h2>
                <TodoList></TodoList>
            </div>
            <div>
                <h2 class='header'>NOTIFICATION</h2>
                <Notification></Notification>
            </div>        
        </div>
    </div>
</template>

<script>
import TodoList from './TodoList.vue';
import Notification from './Notification.vue';

export default {
    components: {
        TodoList,
        Notification
    },
    data() {
        return {

        };
    },
    beforeCreate() {
        document.body.className = 'todo';
    }
}
</script>

<style scoped lang='scss'>
#todoComponents {
    margin: 50px 0;
    display: flex;
    justify-content: center;

    div {
        margin: 0 20px;
    }

    div > h2 {
        font-size: 32px;
        position: relative;
        top: 30px;
        left: 20px;
    }
}

#todoComponents #todoList, #todoComponents #notification {
    margin-top: 30px;
}

@media only screen and (max-width: 1130px) {
  #todoComponents {
    flex-direction: column;
    -ms-flex-direction: column;

    > div {
        margin: 0 auto;
        width: 450px;

        h2.header {
            font-size: 32px;
        }
    }

    #todoList, #notification {
        width: auto;
    }
  }
}

@media only screen and (max-width: 600px) {
    #todoComponents > div h2.header{
        font-size: 28px;
    }

    #todoComponents > div {
        width: 80%;
    }

    #todoList {
        height: 400px;
    }
}

@media only screen and (max-width: 425px) {
    #todoComponents > div h2.header{
        font-size: 22px;
    }
}

@media only screen and (max-width: 380px) {
    #todoComponents {
        > div {
            width: 90%;
        }
    }
}

@media only screen and (max-width: 340px) {
    #todoList {
        height: 350px;
    }
}
</style>