# Godot Reference

## Topics I need to cover

How to save a file

How to publish a game

How to make a sprite have pathfinding

How to add an item in a grid container

How to show the amount of similar items in a item menu

How to create enemy AI

[how to get children nodes from a parent][get_children]

[how to use parallax scrolling][p-scroll]

[tween transition types][trans-type]

[tween ease types][ease-type]

[how to use the tween animation][ani-node]

[how to turn off the collision of a node/object][coll-off]

[How to clear/delete a node from a scene][clear-node]

[How to transition to another scene][trans-scene]

[how to print something to console][print]

[how to get screen size][get-screen]

[how to get a position of a node][get-pos]

[how to get a size of a texture/sprite][size-texture]

[how to check a type of node][check-node]

[how to create an instance of an object][inst-object]

[how to create a timer in gdscript][timer-script]

[inst-object]:#how-to-create-an-instance-of-an-object
[check-node]:#how-to-check-a-type-of-node
[get-children]:#how-to-get-children-from-a-parent
[p-scroll]:#how-to-use-parallax-scrolling
[ease-type]:#tween-ease-types
[trans-type]:#tween-transition-type
[ani-node]:#how-to-animate-a-node
[coll-off]:#how-to-turn-off-the-collision-of-a-node
[clear-node]:#how-to-clear-a-node-from-a-scene
[trans-scene]:#how-to-transition-to-another-scene
[size-texture]:#how-to-get-a-size-of-a-texture-sprite
[get-pos]:#how-to-get-a-position-of-a-node
[get-screen]:#how-to-get-screen-size
[print]:#how-to-print-something-to-console
[home]:#godot-reference

---

### how to create a timer in gdscript

<details>
<summary>
View Content
</summary>


```python
onready var collection = $collection
var timer  = Timer.new() # creates a new instance of a timer

func _ready():
	timer.set_one_shot(true) # make sure the time doesn't repeat
	timer.set_wait_time(5) # set's the countdown time in seconds
	timer.connect("timeout", self, "on_timeout") # when the timer ends it call the function on_timeout
	collection.add_child(timer)#this adds the timer in a node called collection
	timer.start() #this starts the timer when you
	pass

func _process(delta):

	if paused:
		print(timer.time_left) #if paused is true, it will print out the remaining time

	pass



func on_timeout():
	print("foo") # after the time end it will print into the console foo
```

</details>

[go back :house:][home]

### how to create an instance of an object

<details>
<summary>
View Content
</summary>


```python
var brick = bricks.instance()
# If I preloaded an object, this will create the object so that I can put it inside
# the scene
```

</details>

[go back :house:][home]


### how to check a type of node

<details>
<summary>
View Content
</summary>

```python
## this checks if the node is a Position2D type
if node is Position2D :
	print("k")

```

</details>

[go back :house:][home]



### how to get children from a parent

<details>
<summary>
View Content
</summary>

**reference**
- []()

```python
for node in collection.get_children():
	print(node.name)
```

</details>

[go back :house:][home]

### how to use parallax scrolling

<details>
<summary>
View Content
</summary>

**reference**
- [ParallaxLayer](https://docs.godotengine.org/en/3.1/classes/class_parallaxlayer.html#class-parallaxlayer-property-motion-offset)


1. Add a node called ParallaxBackground

2. Select ParallaxBackground and add a child node called ParallaxLayer

3. Select ParallaxLayer and a add child node that can either be a TileMap or a Sprite.

4. In the options of the ParallaxLayer there is an called Scale. It has x and y
coordinates, and this is the place where you will create the parallax effect. If
you want the parallax scrolling to only happen horizontally then change the x coordinate.
The default value is 1, but if you make it less than (for example: 0.5), the parallax effect
will be more apparent.

5. There are other options like mirroring which will duplicate the image in the ParallaxLayer,
and the offset option that position the image. But I haven't really used them that much


</details>

[go back :house:][home]

### tween ease types

<details>
<summary>
View Content
</summary>

**reference**
- [tween class](https://docs.godotengine.org/en/3.0/classes/class_tween.html#class-tween-interpolate-property)

Ease Type | Value
-|-
EASE_IN | 0
EASE_OUT | 1
EASE_IN_OUT | 2
EASE_OUT_IN | 3


</details>

[go back :house:][home]

### tween transition type

<details>
<summary>
View Content
</summary>

**reference**
- [tween class](https://docs.godotengine.org/en/3.0/classes/class_tween.html)

Transition Type | Value
-|-
TRANS_LINEAR | 0
TRANS_SINE | 1
TRANS_QUINT | 2
TRANS_QUART | 3
TRANS_QUAD | 4
TRANS_EXPO | 5
TRANS_ELASTIC | 6
TRANS_CUBIC | 7
TRANS_CIRC | 8
TRANS_BOUNCE | 9
TRANS_BACK | 10



</details>

[go back :house:][home]

### how to use the tween animation

<details>
<summary>
View Content
</summary>

**reference**
- [Tween](https://docs.godotengine.org/en/3.0/classes/class_tween.html#class-tween-interpolate-property)

There are many ways to change the property of a node, so these are a couple of examples of how to change it

**syntax**
`$Tween.interpolate_property(Object, property, initial value, final value, duration time, transition type, ease type, delay time)`

```python
$Tween.interpolate_property($Sprite,"modulate", Color(1,1,1,1), Color(1,1,1,0),0.3, Tween.TRANS_QUAD, Tween.EASE_OUT )
```

</details>

[go back :house:][home]


### how to turn off a collision of a node

<details>
<summary>
View Content
</summary>

**reference**
- [collisionobject2d](https://docs.godotengine.org/en/3.0/classes/class_collisionobject2d.html#class-collisionobject2d-shape-owner-set-disabled)

#### Method 1
```python
# when the potion collides with a body named isaiah
# shape_owner_clear_shapes will clear all the shapes as long as you have the owner id
# which will usually be 0
func _on_potion_body_entered(body):
	if body.get("name") == "isaiah":
		shape_owner_clear_shapes(0)
	pass
```

#### Method 2

```python
# when the potion collides with a body named isaiah
# shape_owner_set_disabled will disable it as long as you have the boolean set to true
# and the owner id of collision shape which will be 0
func _on_potion_body_entered(body):
	if body.get("name") == "isaiah":
		shape_owner_set_disabled(0,true)
	pass
```

</details>

[go back :house:][home]


### how to clear a node from a scene

<details>
<summary>
View Content
</summary>


You usually do this when you are using signals, but I guess you can do that in any
other function

```python
func on_gem_area_enter(area):
  if area.get("name") == "player":
    queue_free() #this will delete the node which is a gem
```

</details>

[go back :house:][home]


### How to transition to another scene

<details>
<summary>
View Content
</summary>

```python
get_tree().change_scene("res://World2.tscn")
```

</details>

[go back :house:][home]



### how to get a size of a texture/sprite

<details>
<summary>
View Content
</summary>

```python
var sprite_size = get_texture().get_size()
```


</details>

[go back :house:][home]


### how to get a position of a node

<details>
<summary>
View Content
</summary>

```python
print(get_pos())
```

</details>

[go back :house:][home]

### how to get screen size

<details>
<summary>
View Content
</summary>


```python
var screensize = get_viewport_rect().size
```

</details>

[go back :house:][home]

### how to print something to console

```python
print("someting to console")
```
