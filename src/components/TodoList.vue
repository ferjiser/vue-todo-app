<template>
 <div id="todoList">
            <ul>
                <li v-for="item in list" :key="item.id" :class="[item.done ? 'done' : '']">
                    <div :class="[`checkBox '${item.done ? ' done' : ''}`]" @click="updateStatusTask(item)"></div>
                    <span>{{item.title}}</span>
                    <i class="fa fa-trash-o" @click="removeTask(item)"></i>
                </li>
            </ul>
            <div id="newTask">
                <input v-model="task" type="text" placeholder="New task" @keyup.enter="addTask">
                <button @click="addTask" ><span>+</span></button>
            </div>
        </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: ['list'],
  data() {
      return {
          task: ''
      }
  },
  methods: {
      addTask(){
        this.$emit('add-task-event', {
            "id": Date.now(),
            "done": false,
            "title": this.task
        });
        this.task = '';
      },
      removeTask(task){
        this.$emit('remove-task-event', task);
      },
      updateStatusTask(task){
        this.$emit('update-task-event', {...task, "done": !task.done});
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#todoList {
    width: 300px;
    box-shadow: -2px 2px 2px -1px rgba(0, 0, 0, 0.15);
    border-radius: 8px;
    background: white;
    overflow: hidden;
}
#todoList ul {
    list-style: none;
    padding: 25px;
}
#todoList ul li {
    display: flex;
    align-items: center;
    line-height: 1;
    user-select: none;
}
#todoList ul li:not(:last-child) {
    padding-bottom: 15px;
}
#todoList ul li:hover {
    cursor: text;
}
#todoList ul li .checkBox {
    width: 20px;
    height: 20px;
    border: 2px solid #ddd4ce;
    border-radius: 50%;
    margin-right: 15px;
    position: relative;
    display: flex;
    opacity: 0.7;
}
#todoList ul li .checkBox:hover {
    cursor: pointer;
    opacity: 1;
}
#todoList ul li .checkBox, #todoList ul li .checkBox:before {
    transition: all 0.2s ease-in-out;
}
#todoList ul li .checkBox:before {
    content: "\f00c";
    font-family: "FontAwesome";
    margin: auto;
    font-size: 0.8em;
    color: #31ecb8;
    opacity: 0;
    transform: scale(0.5);
}
#todoList ul li .checkBox.done {
    border-color: #31ecb8;
    opacity: 1;
}
#todoList ul li .checkBox.done:before {
    opacity: 1;
    transform: scale(1);
}
#todoList ul li i {
    margin-left: auto;
    padding-left: 15px;
    opacity: 0;
    color: #ff3c41;
    transition: all 0.2s ease-in-out;
    font-size: 1.2em;
}
#todoList ul li:hover i {
    opacity: 1;
    cursor: pointer;
}
#todoList ul li span {
    position: relative;
}
#todoList ul li span, #todoList ul li span:before {
    transition: all 0.2s ease-in-out;
}
#todoList ul li span:before {
    content: '';
    height: 1px;
    background: #c3bbb6;
    width: 0%;
    top: 50%;
    position: absolute;
    left: 0;
}
#todoList ul li.done span {
    color: #c3bbb6;
}
#todoList ul li.done span:before {
    width: 100%;
}
#todoList #newTask {
    background: rgba(0, 0, 0, 0.05);
    padding: 15px;
    display: flex;
}
#todoList #newTask input {
    flex: 1;
    margin-right: 10px;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    outline: none;
    border-left: 2px solid #f65050;
    font-family: 'Roboto', sans-serif;
}
#todoList #newTask button {
    outline: none;
    border: none;
    border-radius: 50%;
    font-size: 1.5em;
    color: white;
    background: #f65050;
    display: flex;
    width: 35px;
    height: 35px;
    transition: all 0.15s ease-in-out;
}
#todoList #newTask button span {
    margin: auto;
}
#todoList #newTask button:hover {
    cursor: pointer;
    background: #ff5c60;
}
</style>
