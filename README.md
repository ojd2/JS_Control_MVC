# ABOUT

A simple Todo List Application for the following Dissertation Project for student 150033255.
Also, the application has been created in order to explore and learn more about the MVC pattern.


### THE MODEL

A core entity to represent the space for capturing Todo Tasks submitted by users.

A series of interactions with the core entity such as procedure definitions for adding 
Todo's and selecting Todo's for deletion. These are usually contained within the model 
entity and component.

"Models represent knowledge. A model could be a single object (rather uninteresting), or it
could be some structure of objects. There should be a one-to-one correspondence between the 
model and its parts on the onehand, and the represented world as perceived by the owner of 
the model on the other hand. The nodes of a model should therefore represent an identifiable
part of the problem."  - (Reenskaug,T, 1979)


Declare our empty concrete entity to capture the state. We represent the concrete
entity as an empty array. By using an array we can store all Todo Tasks 
individually and any associated or inherited procedures.

```
function TodoList(){
  this.TodoList = []; 
}
```

When Tasks are entered, use the following procedure to initiate an object.
The object takes the following Task and captures it as an `Obj`. The `Obj` is then
passed onto the concrete entity TodoList above. We can use the prototype method
to do just that.

```
TodoList.prototype.addTaskToList = function( obj ){
  return this.TodoList.push( obj );
};

```
We have a simple removeAt procedure. This is used for when Todo Tasks may 
be selected in order to delete. The following procedure returns the 
concrete entity array and splices the index of the item. The index is assigned
using a simple `indexOf` procedure below.

 ```
TodoList.prototype.removeAt = function( index ){
  this.TodoList.splice( index, 1 );
};
```

Next we have a count prototype procedure that simply keeps track of 
all objects (Todo Tasks) created and stored into our inherited concrete entity.

```
TodoList.prototype.count = function(){
  return this.TodoList.length;
};
```

Our `indexOf` prototype is for identifying our list and designating their 
index numbers. This is mainly for keeping track of all objects (Todo Tasks). 
Simply assigns unique ids `(1 - n)`.

```
TodoList.prototype.indexOf = function( obj, startIndex ){
  var i = startIndex;
  while( i < this.TodoList.length ){
    if( this.TodoList[i] === obj ){
      return i;
    }
    i++;
  }
  return -1;
};
```

### THE CONTROLLER

"The controller receives such user output via the concrete entity (Model), 
it then translates the model behavior into the appropriate messages and passes 
these messages onto one or more of the view procedures below." - (Reenskaug,T, 1979)

Declare our main controller which communicates with the output of the prior 
model. We initiate a new version of the `TodoList()` and push it onto the view
using inherited procedures of the `Controller`.

```
function Controller(){
  this.todos = new TodoList();
}
```

We define the first controller method. This is where users will be able 
to see their inputted Todo Task be passed into the `View` entity below for 
visually displaying the task.

```
Controller.prototype.addTodo = function( todo ){
  this.todos.add( todo );
};
```

A simple procedure to remove Todos from the concrete entity.

```
Controller.prototype.removeTodo = function( todo ){
  We call the previous model procedure removeAt(): 
  this.todos.removeAt( this.projects.indexOf( todo, 0 ) );
};
```

Finally, we extend the procedures into the view using a generic extend procedure.

```
function extend( obj, extension ){
  for ( var key in extension ){
    obj[key] = extension[key];
    console.log(obj[key]);
  }
} 
```

### THE VIEW

"A view is attached to its model (or model part) and gets the data necessary for the presentation
from the model by asking questions. It may also update the model by sending appropriate
messages. All these questions and messages have to be in the terminology of the model, the
view will therefore have to know the semantics of the attributes of the model it represents. (It
may, for example, ask for the model's identifier and expect an instance of Text, it may not
assume that the model is of class Text.)" - (Reenskaug,T, 1979)

We begin with a `AddTodo` procedure. We add each Todo and the extracted value as an `<li>` DOM
element as we have a far more flexibility in manipulating the HTML. 

```
function AddTodo(){
  todo = document.createElement( "li" );
  todo.className = "li-todo";
  todoValue = document.getElementById( "todoValue" );
  value = projectValue.value;
  todo.innerHTML = 'Todo Task: ' + value ;
  // Update the concrete entity state via assigning the value of the Todo
  // task to an actual object todo:
  todo.updateTodo = function( value ){
      this.todo = value;
	};
  // Finally, append the Todo to the HTML DOM:
  container.appendChild(todo);
  // Call a procedure to display the Todos in the Todo list container:
  showTasks();
};
```

Simple procedure to remove an added Todo Task:

```
function RemoveTodo() {
	var selectTodo = document.getElementById("todoValue");
    selectTodo.remove(selectTodo.selectedIndex);
}
```