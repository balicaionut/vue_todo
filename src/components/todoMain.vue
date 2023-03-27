<template>
    <body>
        <main id="app">
            <section class="todo-list">
                <h3>To-do List</h3>
                <div class="all-todos">
                    <div class="single-todo done">
                        <p>Learn HTML, CSS and Javascript</p>
                    </div>
                    <div class="single-todo done">
                        <p>Learn the basics of Vue JS</p>
                    </div>
                    <div class="single-todo">
                        <p>Complete Vue JS Challenge with excellence</p>
                    </div>
                </div>
                <button class="clear">Clear All</button>
                <label for="todoAdd">Add new todo <input type="text" id="todoAdd"></label>
                <button class="add">Add</button>
                <div class="instructions">
                    Instructions:
                    <ul>
                        <li>Click the to-do text to toggle between done / undone</li>
                        <li>Use clear all button to remove all items</li>
                        <li>Use the input field to add new to-dos</li>
                    </ul>
                </div>
            </section>
        </main>
    </body>
</template>

<script>
export default {

};
</script>

<style>
@import '../assets/css/style.css';
</style>
