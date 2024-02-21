# Basic Movement

Right click sprites to create a new sprite

Click on the first frame of the sprite (at the bottom) to bring up the sprite editor

Image > *Resize all frames* > *Resize Canvas* to resize the sprite

Right click objects to create an object

Rooms are places where you can put your different objects

The **instances** layer are objects that have actually been placed into the game

Click the instances layer, and then click the object you want to place - hold **alt** and you then will be able to click to place an instance of that object in the game

Resize the room size in the bottom left properties box

The viewport is how big the window will be when you run the game

Make sure to enable viewport 0 to start

Set the camera width and height to the same size as your room

The viewport width and height will then determine the actual width and height of the game on the screen in pixels
- So make sure to multiply the width and height of the camera properties by some integer - to avoid scaling problems

Add events to an object to have them run code

The **step** event runs every frame of the game

Basic movement detection for step:

```gml
var _right_key = keyboard_check(vk_right);
var _left_key = keyboard_check(vk_left);
var _up_key = keyboard_check(vk_up);
var _down_key = keyboard_check(vk_down);

xspd = (_right_key - _left_key) * move_spd;
yspd = (_down_key - _up_key) * move_spd;

x += xspd;
y += yspd;
```

`xspd` and `yspd` are set in the **create** event

# Collision

The anchor point on the sprite shows where the origin point is

The bottom left section of the sprite menu has a section called *Collision Mask*

You can manually set a collision mask or have it set to the size of the sprite image

Use `place_meeting` to check if there is a collision between two objects

```gml
var _right_key = keyboard_check(vk_right);
var _left_key = keyboard_check(vk_left);
var _up_key = keyboard_check(vk_up);
var _down_key = keyboard_check(vk_down);

xspd = (_right_key - _left_key) * move_spd;
yspd = (_down_key - _up_key) * move_spd;

if place_meeting(x + xspd, y, obj_wall) == true {
	xspd = 0;
}

if place_meeting(x, y + yspd, obj_wall) == true {
	yspd = 0;
}

x += xspd;
y += yspd;
```

# Animation

At the top of the sprite image editor you can create more frames

The small drop down tab beneath frames will let you change the frame speed

Duplicate your sprites and rotate them to have four different sprites for each direction a character can walk

Use *Image* > *Rotate All Frame (clockwise 90)*

Use the *Scripts* folder to create some constants

```gml
#macro RIGHT 0
#macro UP 1
#macro LEFT 2
#macro DOWN 3
```

Create an array in the *create* event to hold the direction sprites

```gml
sprite[RIGHT] = spr_player_right;
sprite[UP] = spr_player_up;
sprite[LEFT] = spr_player_left;
sprite[DOWN] = spr_player_down;

face = DOWN
```

Use a variable to keep track of the current direction

Set the sprite with **sprite_index**

```gml
sprite_index = sprite[face]
```

To determine the direction you are facing:

```gml
if yspd == 0 {
	if xspd > 0 {face = RIGHT};
	if xspd < 0 {face = LEFT};
}
if xspd > 0 && face == LEFT {face = RIGHT};
if xspd < 0 && face == RIGHT {face = LEFT};
if xspd == 0 {
	if yspd > 0 {face = DOWN};
	if yspd < 0 {face = UP};
}
if yspd > 0 && face == UP {face = DOWN};
if yspd < 0 && face == DOWN {face = UP};
sprite_index = sprite[face];
```

To stop a character from animating when they are not moving:

```gml
if xspd == 0 && yspd == 0 {
	image_index = 0;
}
```

This will set the sprite image to the first frame whenever the character stops moving

Full code:

```gml
var _right_key = keyboard_check(vk_right);
var _left_key = keyboard_check(vk_left);
var _up_key = keyboard_check(vk_up);
var _down_key = keyboard_check(vk_down);

xspd = (_right_key - _left_key) * move_spd;
yspd = (_down_key - _up_key) * move_spd;


if yspd == 0 {
	if xspd > 0 {face = RIGHT};
	if xspd < 0 {face = LEFT};
}
if xspd > 0 && face == LEFT {face = RIGHT};
if xspd < 0 && face == RIGHT {face = LEFT};
if xspd == 0 {
	if yspd > 0 {face = DOWN};
	if yspd < 0 {face = UP};
}
if yspd > 0 && face == UP {face = DOWN};
if yspd < 0 && face == DOWN {face = UP};
sprite_index = sprite[face];


if place_meeting(x + xspd, y, obj_wall) == true {
	xspd = 0;
}

if place_meeting(x, y + yspd, obj_wall) == true {
	yspd = 0;
}


x += xspd;
y += yspd;


if xspd == 0 && yspd == 0 {
	image_index = 0;
}

```