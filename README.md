# Game Maker Studio 2 - Physics Library STARDUST Instructions

Instructions on how to use STARDUST physics library.

<# #> - info

/// - example

[ ] - optional

For library examples check out "Demos" folder.

Inside Stardust -> global_physics_object -> create event: you can customize your physics global proerties.

Project Setup: (You can delete "Demos" folder if you don't need it)

Create an object, you can call it whatever you want (example: physics, obj_physics)

Inside physics object add "Create Event" and write: physics_init();

<# physics_init() - it will just create "global_physics_object" where some physics data is stored. #>

After that you just need to drag physics object into a room.

Make sure from rooms "Instance Creation Order" physics object is at the top.

Now you can use STARDUST functions.

Functions:

1) ------------ create_object(mass, id, COR) ------------

mass -> objects mass

id -> objects "id"

COR -> coefficient of restitution (number between 0 - 1, it is how bouncy an object is)

This function returns an physics object with mass, speed and other physics properties.

example:

///

object = create_object(2, id, 0.8);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Objects -> create_object

2) ------------ create_static(id) ------------

id -> objects "id"

This function adds object into statics array. this means physics objects will be able to collide

with this static object.

example:

///

create_static(id);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Objects -> create_static

3) ------------ render_motion(object, [enable_friction], [enable_collisions], [enable_water_collisions]) ------------

object -> physics object

[enable_friction] * optional -> enables friction | DEFAULT: false

[enable_collisions] * optional -> enables collisions | DEFAULT: false

[enable_water_collisions] * optional -> enables water collisions | DEFAULT: false

This function calculates every force on physics objects and moves it.

example:

///

render_motion(object, true, true, false);

///

Must Be Placed In: Step Event (or any loop)

Source: StarDust -> Physics -> Motion -> render_motion

4) ------------ add_force(object, force, direction) ------------

object -> physics object

force -> force magnitude

direction -> direction to apply

This function adds force to physics object.

example:

///

add_force(object, 100, 45);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Force -> add_force

<# next up is "force_ctrl" so let me explain something. force_ctrl means force control. its used to create a different kind

of force which direction and force magnitude can be changed. previous "add_force" function after creating it you can't

delete or change its direction, its permament.s #>

5) ------------ add_force_ctrl(object, force, direction) ------------

object -> physics object

force -> force magnitude

direction -> direction to apply

This function returns force ctrl object so you can apply it to object or change its properties.

example:

///

force = add_force_ctrl(object, 100, 45);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Force - Control -> add_force_ctrl

6) ------------ apply_force_ctrl(object, force_ctrl) ------------

object -> physics object

force_ctrl -> force ctrl object

This function applies force_ctrl to object. Must be done once after creating force_ctrl.

example:

///

force = add_force_ctrl(object, 100, 45);

apply_force_ctrl(object, force);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Force - Control -> apply_force_ctrl

7) ------------ remove_force_ctrl(object, force_ctrl) ------------

object -> physics object

force_ctrl -> force ctrl object

This function removes force object from object.

example:

///

force = add_force_ctrl(object, 100, 45);

remove_force_ctrl(object, force);

///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Force - Control -> remove_force_ctrl

8) ------------ set_force_ctrl_dir(object, force_ctrl, direction) ------------

object -> physics object

force_ctrl -> force ctrl object

direction -> direction to set

This function changes force ctrl object direction to desired direction and returns new changed force.

example:

///

force = add_force_ctrl(object, 100, 45);

force = set_force_ctrl_dir(object, force, 0);

///

Must Be Placed In: Anywhere

Source: StarDust -> Physics -> Force - Control -> set_force_ctrl_dir

9) ------------ set_force_ctrl_force(object, force_ctrl, new_force) ------------

object -> physics object

force_ctrl -> force ctrl object

new_force -> force magnitude to set

This function changes force ctrl object force magnitude to desired magnitude and returns new changed force.

example:

///

force = add_force_ctrl(object, 100, 45);

force = set_force_ctrl_force(object, force, 50);

///

Must Be Placed In: Anywhere

Source: StarDust -> Physics -> Force - Control -> set_force_ctrl_force

10) ------------ display_vectors(object, scale, [draw_force], [draw_impulse], [draw_friction], [draw_motion]) ------------

object -> physics object

scale -> vector scale

[draw_force] * optional -> draw forces | DEFAULT: false

[draw_impulse] * optional -> draw impulses | DEFAULT: false

[draw_friction] * optional -> draw friction | DEFAULT: false

[draw_motion] * optional -> draw motion | DEFAULT: false

This function draws forces, impulses, friction and objects motion.

example:

///

display_vectors(object, 1, true, true, true, false);

///

Must Be Placed In: Draw Events (or draw functions)

Source: StarDust -> Physics -> Debug -> display_vectors | and | StarDust -> Physics -> Debug - Sprites

11) ------------ set_gravity(object, gravity) ------------

object -> physics object

gravity -> gravity to apply

This function adds gravity force on object.

example:

///

set_gravity(object, phy.grav);

///

You may wonder what does "phy.grav" mean. "phy" is just a macro and it is "global_physics_object".

So in reality it means "global_physics_object.grav".

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Gravity -> set_gravity | and | StarDust -> Physics -> global_physics_object | and | StarDust -> Physics -> Macros

12) ------------ gs_add_planet(object) ------------
object -> physics object

This function creates planet from physics object, and adds it into planets array.

example:
///
planet = gs_add_planet(object);
///

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Gravitational Systems -> gs_add_planet

13) ------------ gs_update(object) ------------

object -> physics object

This function goes through planets array and applies some gravity physics.

example:

///

gs_update(object);

///

Must Be Placed In: Step Event (or any loop)

Source: StarDust -> Physics -> Gravitational Systems -> gs_update

14) ------------ create_liquid(id, x, y, width, height, speed, detail, wave_width, wave_height, density, [interact_enable]) ------------

id -> objects "id"

x -> objects x position

y -> objects y position

width -> objects image_xscale

height -> objects image_ysacle

speed -> wave speed

wave_width -> wave width

wave_height -> wave height

density -> liquid density

[interact_enable] * optional -> enable liquid collision | DEFAULT: false

This function creates liquid object with its properties and returns it.

example:

///

water = create_liquid(id, x, y, image_xscale, image_yscale, 0.5, 20, 30, 10, 1000, true);

///

Make sure you make seperate object for liquids in gamemaker. And make sure you use "spr_sd_water_editor" sprite which is located at:

StarDust -> Physics -> Water - Texture -> spr_sd_water_editor.

And however you place it in your editor, it will be shown like that in game. (but you need to use "draw_liquid" function which is next)

Must Be Placed In: Create Event (or must be run once)

Source: StarDust -> Physics -> Water -> create_liquid

15) ------------ draw_liquid(liquid_obj, [water_shader], [prim]) ------------

liquid_obj -> liquid object

[water_shader] * optional -> water shader | DEFAULT: sh_sd_water

[prim] * optional -> prim | DEFAULT: pr_trianglelist

This function draws liquid with its properties.

example:

///

draw_liquid(water, sh_sd_water, pr_trianglelist);

///

Must Be Placed In: Draw Event (or draw functions)

Source: StarDust -> Physics -> Water -> draw_liquid | and | StarDust -> Physics -> Shaders | and | StarDust -> Physics -> Vertex

--------------------------------------------------------------------------------------------------------------------------------------------
Phyics Library - STARDUST

Description:
STARDUST is a physics library developed by GeoStarGames.
It provides Impulse, Forces, Gravity, Water Physics.

License:
STARDUST is the intellectual property of GeoStarGames. All rights reserved.
Unauthorized distribution or reproduction of this library, or any portion of it, is prohibited.

Contact:
For support or inquiries, please contact GeoStarGames at geostargamesnw@gmail.com

Copyright © GeoStarGames 2024. All Rights Reserved.
