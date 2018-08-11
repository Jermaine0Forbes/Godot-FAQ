# Logs 

## 8/11/18

```python
extends Node

# class member variables go here, for example:
# var a = 2
# var b = "textvar"
onready var timer = get_node("Timer")
onready var label = get_node("Label")
onready var app = preload("res://objects/apple.tscn")
onready var sound = get_node("sound")
onready var prize = get_node("prize")
onready var spawn1 = get_node("spawn_1")
onready var spawn2 = get_node("spawn_2")
onready var spawn3 = get_node("spawn_3")
var spawns 
signal item_collect
var screensize
var apple
#onready var menu = get_node("menu3")
#var menu_open = false

func _ready():
	timer.set_wait_time(30)
	timer.set_one_shot(true)
	timer.connect("timeout",self, "on_timeout")
	timer.start()
	apple = app.instance()
	apple.connect("apple_contact", self, "_contact_sound")
	prize.connect("victory", self , "on_victory")
	sound.get_node("myrrh").connect("finished", self,"change_scene")
	screensize = get_viewport().get_visible_rect().size
	spawns = {1:spawn1, 2:spawn2, 3:spawn3}
	spawn_items(8)

	#menu.hide()
	
	# Initialization here
	pass

#func _process(delta):
#	# Called every frame. Delta is time since last frame.
#	# Update game logic here.
#
#
##	is_open()
#
#
#	pass

func spawn_items(num):
	for i in range(num):
		var a = app.instance()
		var x = randi()%3+1
		print("spawn"+str(x))
		var spawn = spawns[x]
		var size = spawn.get_global_position()
		spawn.add_child(a)
#		a.set_position(Vector2(rand_range(10, size.x-10),rand_range(10, size.y-10)) )
#		a.set_position(size)
#		a.setPos(get_global_pos()+Vector2(randf()*6-3,randf()*6-3) )
		a.connect("apple_contact", self, "_contact_sound")
		

func change_scene():
	get_tree().change_scene("res://World2.tscn")

func on_victory():
	sound.get_node("myrrh").play()
	

func _contact_sound():
#	print(apple.get_node("Sprite").get_texture().load_path)
	emit_signal("item_collect", apple.get_node("Sprite").get_texture().load_path)
	sound.get_node("item").play()
	

func update_time():
	var x = int(timer.time_left)
	if x > 0 :
		var text =  "0:0"+str(x) if x < 10 else "0:"+str(x)
		label.set_text(text)
	

func on_timeout():
	print("timer has stopped")
	

#func is_open():
#	if Input.is_action_just_pressed("ui_accept") and menu_open == false:
#		menu.show()
#		print("im calling you")
#		menu_open = true
#		get_tree().paused = true
#	elif Input.is_action_just_pressed("ui_accept") and menu_open == true:
#		menu.hide()
#		menu_open = false
#		get_tree().paused = false


```


## 8/5/18

### Update 

```python
extends Control

onready var item_slots = $items
onready var cir_btn = $circle
onready var ico_btn = $icon
var circ_path 
var icon_path
var items = {}


func _ready():
	set_items()
#	print(items)
	pass

#func _process(delta):
#	# Called every frame. Delta is time since last frame.
#	# Update game logic here.
#	pass

func get_next_empty_slot():
	var slot
	for i in items.keys():
		if items[i][0] == null or items[i][0] == "" :
			slot = i
			print("slot: "+slot)
			break
	
	return slot

func set_items():
#	item_slots = $items
	for i in item_slots.get_children():
		var name = i.get_name()
		var texture = i.get_node("item").get_texture() 
		var item = texture.load_path if texture !=null else ""
		var count = i.get_node("count").get_text()
		
		items[name] = [item,count]
		
	

func add_item(item):
	var num 
	var slot
	var text
	var next_slot
	var is_item_new = false
	for key in items.keys():
		slot = item_slots.get_node(key)
		if items[key][0] == item:
			if not items[key][1]:
				num = 1
			else:
				num = int(items[key][1])+1
#			get_node(key).get_node("count").set_text(num+1)
			print(num)
			text = str(num)
			slot.get_node("count").set_text(text)
#			items[key][1] = int(text)
			set_items()
			is_item_new = false
			break
		else :
			is_item_new = true
	
	if is_item_new :
		next_slot = get_next_empty_slot()
		print(next_slot)
		var t = load(item) 
		item_slots.get_node(next_slot).get_node("item").set_texture(t)
		set_items()
	
	pass


func _on_circle_pressed():
	circ_path = cir_btn.get_normal_texture().load_path
	add_item(circ_path)
	pass # replace with function body


func _on_icon_pressed():
	icon_path = ico_btn.get_normal_texture().load_path
	add_item(icon_path)
	pass # replace with function body


```


## 8/4/18

### What I've been working on 

```python

extends Control

onready var item_slots = $items
onready var cir_btn = $circle
onready var ico_btn = $icon
var circ_path 
var icon_path
var items = {}


func _ready():
	set_items()
#	print(items)
	pass

#func _process(delta):
#	# Called every frame. Delta is time since last frame.
#	# Update game logic here.
#	pass

func get_next_empty_slot():
	var slot
	for i in items.keys():
		if items[i][0] == null or items[i][0] == "" :
			slot = i
			print("slot: "+slot)
			break
	
	return slot

func set_items():
	for i in item_slots.get_children():
		var name = i.get_name()
		var texture = i.get_node("item").get_texture() 
		var item = texture.load_path if texture !=null else ""
		var count = i.get_node("count").get_text()
		
		items[name] = [item,count]
		
	

func add_item(item):
	var num 
	var slot
	var text
	var next_slot
	for key in items.keys():
		slot = item_slots.get_node(key)
		if items[key][0] == item:
			if not items[key][1]:
				num = 0
			else:
				num = items[key][1]
#			get_node(key).get_node("count").set_text(num+1)
			text = str(num+1)
			slot.get_node("count").set_text(text)
			items[key][1] = int(text)
		else :
			next_slot = get_next_empty_slot()
			print(next_slot)
			var t = load(item) 
			item_slots.get_node(next_slot).get_node("item").set_texture(t)
			set_items()
	
	pass


func _on_circle_pressed():
	circ_path = cir_btn.get_normal_texture().load_path
	add_item(circ_path)
	pass # replace with function body


func _on_icon_pressed():
	icon_path = ico_btn.get_normal_texture().load_path
	add_item(icon_path)
	pass # replace with function body


```

## 7/28/18

### Best way to add items in ItemList

**reference**
- [godotengine](https://godotengine.org/qa/24147/best-way-to-add-items-in-itemlist)

```python
extends Node

onready var itemList = get_node("itemlist")
onready var items = preload("res://atlas.tres")
onready var items_amount = 4
onready var items_width = 50
onready var items_height = 50

func _ready():
    itemList.max_columns = 9
    itemList.fixed_icon_size = Vector2(32,32)
    itemList.icon_mode = ItemList.ICON_MODE_TOP
    itemList.select_mode = ItemList.SELECT_SINGLE
    itemList.same_column_width = true

    for i in range(items_amount):
        var item = items.duplicate()
        item.set_region(Rect2(i * items_width, 0, items_width, items_height))
        itemList.add_item("", item, true)
```
