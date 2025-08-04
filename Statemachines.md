Some code here
```
class_name Player #This makes the script usable in editor and other scripts with name Player
extends CharacterBody2D

@onready #@onready means that this line runs when the node enters the scene tree. So node exists.
var animations = $animations
#So basically, sets up a variable called animations that points to the node animations.

@onready
var state_machine = $state_machine
# This references the state machine node 

func _ready() -> void:
	///Initialize the state machine, passing a reference of the player to the states,
	//that way they can move and react accordingly
	state_machine.init(self)
#This initializes the state macine and passes the player node instance to it. In order for the statemachine to control the player

func _unhandled_input(event: InputEvent) -> void:
	state_machine.process_input(event)
#This sends input events to the statemachine to handle them

func _physics_process(delta: float) -> void:
	state_machine.process_physics(delta)
#This passes the delta time to the state machine to update phycis related logic

func _process(delta: float) -> void:
	state_machine.process_frame(delta)
#It allows the statemachine to update anything that needs to happen every frame.
```
