# Logs 


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
