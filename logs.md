# Logs 

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
