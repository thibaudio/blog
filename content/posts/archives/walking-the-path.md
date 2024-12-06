---
title: "Walking the path"
date: 2022-09-25T22:07:58+02:00
draft: false
toc: false
images:
tags:
---

Hi friends, I hope you all had a great week and weekend!

This week I've made some progress on my Little Red Riding Hood puzzle game, it's now a fully functioning game, with 2 levels.
I still have a lot to do before I can call that a finished product though:
- [X] Turn based actions
- [X] Wolf pathfinding
- [X] Loose condition
- [X] Obstacles
- [X] Door
- [X] Opening the door with Wolf -> Loose as well
- [X] Hunter kills wolf
- [ ] Transitions
- [ ] Menu
- [ ] Options
- [ ] Save
- [ ] 5 levels
- [ ] Win screen
- [ ] In game menu
- [ ] Better death animation
- [ ] Better indication that we need to kill the wolf before escaping
- [ ] Sounds
- [ ] Music
- [ ] Tutorial, Dialogs

## Building on Heartbeast A* pathfinding
To implement my wolf pathfinding, I used HeartBeast's [Astar Implementation Script for TileMap Nodes in Godot](https://github.com/uheartbeast/astar-tilemap).
The debug is view is really neat, and the script easy to build from.
I had to modify it slightly for my use case: 

### Indexing cells by their grid position
In the original script, all the cells, units and obstacle are indexed using their real world position.  
Let's focus on the cells:
```gdscript
func create_pathfinding_points() -> void:
	astar.clear()
	var used_cell_positions = get_used_cell_global_positions()
	for cell_position in used_cell_positions:
		astar.add_point(get_point(cell_position), cell_position)

func get_used_cell_global_positions() -> Array:
	var cells = get_used_cells()
	var cell_positions := []
	for cell in cells:
		var cell_position := global_position + map_to_world(cell)
		cell_positions.append(cell_position)
	return cell_positions
```

I'm now indexing only based on the cell position in the grid:
```gdscript
func create_pathfinding_points() -> void:
	astar.clear()
	#var used_cell_positions = get_used_cell_global_positions()
	var used_cell_positions = get_used_cells()
	for cell_position in used_cell_positions:
		var cell_world_position = global_position + map_to_world(cell_position) + cell_size/2
		astar.add_point(get_point(cell_position), cell_world_position)
```
I also took the opportunity to register the center of the cell directly, as it's what I found myself needing the most.

### Movement
The movement is heavily inspired by this [tutorial by GDQuest](https://www.youtube.com/watch?v=9laHKHYNyXc), but instead of directly checking if the point is walkable, I'm using the paths built with astar:
```gdscript
func _process(delta):
	var input_direction = get_input_direction()
	if not input_direction:
		return
		
	var cell_start = Grid.world_to_map(position)
	var cell_target = cell_start + input_direction
	var path_points = Grid.get_astar_path_avoiding_obstacles(cell_start, cell_target)
	if len(path_points) > 1:
		move_to(path_points[1])
	else:
		bump()
```

### Objects
I also needed to have interactable objects on the grid, so I'm registering them exactly like the obstacles:
```gdscript
func add_object(object: Object) -> void:
	objects[get_point(world_to_map(object.position))] = object
	if not object.is_connected("tree_exiting", self, "remove_object"):
		object.connect("tree_exiting", self, "remove_object", [object])
				
func remove_object(object: Object) -> void:
	objects.erase(object)
```

And then in the movement script above I'm adding:
```gdscript
	var path_points = Grid.get_astar_path_avoiding_obstacles(cell_start, cell_target)
	if len(path_points) > 1:
		move_to(path_points[1])
		var object = Grid.get_object_on_cell(position)
		if object:
			object.interact()
```


## Some links
Before I let you go, here are some interesting links I came across this week:
- [A nice threadorial on customizable transition shader](https://twitter.com/jumpquestgame/status/1573383293269155840)
- A GDC talk on [Growing Your Code Library with Each New Project](https://www.youtube.com/watch?v=o3X8IvJksGA) including some advices I definitively plan on implementing as I build my games

&nbsp;  
  
All right, that's all for this week.  
It has a bit heavier on the code side than usual, I hope it was your cup of tea!

Thanks for reading and see you next week!