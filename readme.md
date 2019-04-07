# Godot Reference

## Topics I need to cover

How to save a file

How to publish a game

How to make a sprite have pathfinding

How to add an item in a grid container

How to create enemy AI

[How to clear/delete a node from a scene][clear_node]

[How to transition to another scene][trans-scene]

[how to print something to console][print]

[how to get screen size][get-screen]

[how to get a position of a node][get-pos]

[how to get a size of a texture/sprite][size-texture]

[clear-node]:#how-to-clear-a-node-from-a-scene
[trans-scene]:#how-to-transition-to-another-scene
[size-texture]:#how-to-get-a-size-of-a-texture-sprite
[get-pos]:#how-to-get-a-position-of-a-node
[get-screen]:#how-to-get-screen-size
[print]:#how-to-print-something-to-console
[home]:#godot-reference


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
var sprite_size = get_texture().get_size()
```

</details>

[go back :house:][home]

### how to print something to console

```python
print("someting to console")
```
