Creating the Player
==================

In this part of the tutorial, we'll create a player, add animations, and basic movement.
By the end of this section, you should have all of this:

.. image:: img/playerDemo.gif

.. _init-player:

Player Initialization
------------------------

To begin, we'll create a ``CharacterBody2D``. This is a 2D node used to create characters that can move.
In the top left of the scene tree, create a new scene by clicking the **Other Node** button or the **+** button. Add a ``CharacterBody2D``.
The CharacterBody2D node should appear in the tree, and the editor should be in 2D mode.
First, save your new scene by pressing ``Ctrl+S``.
You can create a ``scenes`` folder in your project and save the player scene there, naming it ``player.tscn``.

To the right of ``CharacterBody2D``, you should see a warning icon. If you hover your mouse over it, you will see the following message:

.. image:: img/characterbody2dwarning.png

.. warning::
   * *"This node has no shape, so it cannot collide or interact with other objects.
   Consider adding a *``CollisionShape2D`` *or a *``CollisionPolygon2D`` *as a child to define its shape."*

With that said, let's add a ``CollisionShape2D`` by clicking the **+** icon in the top left, pressing ``Ctrl+A``, or by: **Right-clicking -> Add Node** on the ``CharacterBody2D``.

The ``CollisionShape2D`` node is used to add hitboxes (collision boxes). This is what will allow our player to physically interact with the world around them.
After adding the CollisionShape2D, you should see another warning saying that it doesn't have a shape.

To add a shape, click on the CollisionShape2D node. You'll then see the inspector on the right side of the screen display information about the CollisionShape2D.
Add a ``CapsuleShape2D`` to the ``shape`` attribute, which is normally empty. You should see a sort of blue Tic Tac™ in the middle of your screen; that's the shape you just added:

.. image:: img/collisionsshape.png

You can change its size with the small orange circles, but we'll do that a little later.

.. _init-anims:

Creating Animations
---------------------

Now we have a player consisting of a ``CharacterBody2D`` and a ``CollisionShape2D``. We're missing some visuals!
So we're going to add a sprite to our player.

.. note::
   A *sprite* is simply a 2D texture, used to represent a character, a background, basically anything you see on the screen in a 2D game.

We want our player to have animations, so add an ``AnimatedSprite2D`` node to the player.

Be careful that the node is a child of the ``CharacterBody2D``, and not of the ``CollisionShape2D``. Indeed, we don't want to add a sprite to our collision detection but to our player.
If the node is misplaced in the tree, you can drag and drop it (press and hold on the node and drag it) onto the player node.

You can also rename the player node to ``Player``. After that, you should have a tree structure like this:

.. image:: img/playerscene.png

Another warning! This time about the ``AnimatedSprite2D``. So add a ``SpriteFrame``, as the warning recommends.

.. tip::
   To add a new ``SpriteFrame``, first click on the AnimatedSprite2D in the tree.
   You will then have access to the node's properties in the Inspector, which is located on the right side of your window.

After adding a new SpriteFrame, a new window should appear at the bottom of your screen.
If not, click on the ``SpriteFrames`` you just created in the Inspector.

.. image:: img/spriteframesopened.png

This window is the Animation Editor. You can close and reopen it by clicking on *SpriteFrames* at the bottom of the screen.
On the left, you will find a list of all available animations. Currently, there is only one, called ``default``.
Rename it ``idle``.

.. note::
   An idle animation is the animation that plays when the character is not moving.
   Generally, it depicts the character breathing, looking around a bit, to add movement to the image and bring the game to life.
   In some games, if you wait long enough, special animations will play: the character scratching their head, sitting on the ground, or falling asleep..

Then click on the grid icon: *Add frames from sprite sheet*, and open the file ``assets/player.png``.

.. note:: 
   A spritesheet is an image file that contains all the animation frames for an object.
   This allows you to have only one file, instead of multiple files, saving space and making animation editing easier.

This will open the *Spritesheet Cutter*, which will look like this:

.. image:: img/spritesheetCutter.png

The spritesheet forms a grid where each frame of the animation is placed in a cell.
You can then set the number of frames per column **[1]** and the number of frames per row **[2]**. In our example, we have 6 columns and 8 rows.

Once the frames are aligned with the grid **[3]**, you can select the first 6 frames (the entire first row) by clicking on them in order or by pressing and holding.
Finally, you can click *Add 6 Frames* at the bottom to add the frames to your idle animation.
You should see the selected frames appear in the editor at the bottom:

.. image:: img/spriteframesIdle.png

Now you can play the animation by pressing **play** **[1]**,
and change the animation speed by changing its **FPS** (Frames Per Second) **[2]**.

An idle animation is fine, but we'd like our player to be able to move,
so we'll add a running animation.

To do this, press **Add Animation** in the top left of the `SpriteFrames` window.
Rename this animation ``"run"``, and repeat the same steps as for the idle animation,
selecting the next 6 frames (the entire second row).

For smoother gameplay, you can set both animations to **8 FPS** (or adjust the speed to your preference).

Finally, you can adjust the hitbox created :ref:`earlier<init-player>` to fit our sprite.

.. tip:: 
   To adjust the collision size more easily, you can drag the ``CollisionShape2D`` below the ``AnimatedSprite2D`` in the scene. 
   Nodes that are **below** in the tree will appear **above** in the editor (because they are created afterward and are therefore rendered on top).
   You can then move the ``CollisionShape2D`` back to its original position. This isn't very important, as it won't be visible once the game is launched.

.. image:: img/playerspriteandcollision.png

.. note:: It's generally best to have a hitbox that's slightly smaller than the character's appearance.
   This avoids situations like: *"But* **#@!$&** *I shouldn't have died there, the enemy didn't even touch me, it's ridiculous, this game is so bad!"*

.. _move-init:

Movements Creation
-----------------------

Currently, we have a player with animations, but who doesn't do much.
If you launch the scene with **F6** or by clicking on the **Clap icon with a small triangle** in the top right corner, you'll see your player in a corner of the screen who can't move.
In this section, we'll add some basic movements.

Creating the Script
~~~~~~~~~~~~~~~~~~

To do this, we'll need to use some code snippets.
First, we'll attach a script to the Player by selecting the ``CharacterBody2D`` in the hierarchy,
and clicking on the **scroll-shaped icon**: `Attach a new or existing script to the selected node` at the top of the hierarchy window
(or **Right-click -> Attach Script**).

This pop-up will then open:

.. image:: img/createplayerscript.png

You will need to:

1. Uncheck the template box
2. Specify the location where your script will be stored. Create a folder named ``"scripts"`` and place the ``"player.gd"`` script in it, as shown in the example.

Confirm, and your editor will switch to **Script** mode to open the created file:

.. image:: img/playerEmptyScript.png

Introduction to GDScript
~~~~~~~~~~~~~~~~~~~~~~

The created file is in GDScript, the scripting language used by Godot.
This language is very similar to Python, so if you have some experience with Python,
you should be quite comfortable with GDScript.

Here we will look at the essential elements of this language: **variables** and **functions**

**Variables:**

To create a variable, you must write:

.. code-block:: gdscript

   var variable_name = value

In GDScript, variables are not typed, meaning they can change type, just like in Python.
For example, we can write:

.. code::gdscript

   var x = 1 # x is of type int (integer)
   x = ``hello`` # x is a string (character string)

It is preferable to type your variables for several reasons:

- Avoid type errors (don't do anything wrong with your variables, as in the previous example)
- Give your editor an indication of the type of your variable, so it can suggest relevant information
- Optimize the code (code with typed variables will normally be faster than untyped code)

The syntax is as follows:

.. code-block::gdscript

   var name:type = value
   # Examples
   var x: int = 1
   var y: String = "hello"
   x = "hi" # Error, you cannot assign a value of type "String" to a "int".

Finally, you can *"export"* your variables,
making them editable from the Inspector, by adding ``@export`` before them:

.. code-block:: gdscript

   @export var nom_variable:type = value

.. warning::
   Careful, you cannot *export* variables defined within functions.

**Functions**

To create a function, you must write:

.. code-block:: gdscript

    func function_name(var1, var2, ...):
        # ...
        return var3

This syntax is very similar to that of Python.
If you want to specify the types of your functions, you can do this:

.. code-block:: gdscript

    func function_name(var1:type1, var2:type2, ...)->returnType:
        # ...
        return var3 # var3 is of type returnType
        # if you don't want to return anything, put void instead of returnType
        # In this case you can write just "return" with nothing behind it, or ommit the "return" completely

You will sometimes use predefined functions, such as ``_ready()`` or ``_physics_process(delta)``,
these are functions used by Godot and called at specific times.
These functions allow you to execute a piece of code at a specific time.
For example:
- The ``_ready`` function is called once when your object is added to your game.
- The ``_physics_process(delta)`` function is called each time Godot recalculates its physics (by default: 60 times per second, regardless of the current frame rate).
   The ``delta`` parameter represents the time (in seconds) since the last call.
- The ``_process(delta)`` function is called every frame (different from ``_physics_process``, as it depends on the frame rate).
   The ``delta`` parameter represents the time (in seconds) since the last call (from the last frame).

Rudimentary Movement Implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In practice, to move our player, we need several things:

1. Detect where the player wants to move with each physics update
2. Modify the player's velocity
3. Make the player move and handle collisions with other elements

For this, we can use the following code:

.. code-block:: GDScript

   func _physics_process(delta: float) -> void:
       var directionX:float = Input.get_axis("ui_left", "ui_right")
       velocity.x = directionX * 300.0
       move_and_slide()

This code is inside the ``_physics_process`` function and will therefore execute with each physics engine update.
With each call, we initialize a variable direction, which will take as its value the return value of ``Input.get_axis("ui_left", "ui_right")``

``Input.get_axis(input1, input2)`` is a function that takes two inputs and simulates a joystick between them, indicating its position.
If the joystick is to the left (i.e., input1 is pressed), the function will return -1;
if the joystick is to the right, it will return 1;
otherwise, it will return 0 (if you are using a joystick, you can get all values ​​between -1 and 1, but if you are using a keyboard, you will only get integer values).

Next, after retrieving the player's direction on the X-axis,
we can change the player's velocity on the X-axis by
multiplying the direction by `300.0`, where `300.0` is the speed we want to give our player.

Finally, we are working with a ``CharacterBody2D``, and therefore we have access to the ``move_and_slide()`` function,
which will automatically move the player and handle collisions.

To test this code, you can press ``F6`` (or ``fn+F6``) to run the current scene.

.. hint:: Exercise: Move the player vertically
   Now that you know how to move the player along the X-axis, try (without looking at the rest) to move them
   along the Y-axis.
   Hint: the inputs for up and down are respectively ``"ui_up"`` and ``"ui_down"``

Once we've made the movements along one axis, it's easy to transpose them to the other axis:

.. code-block:: gdscript

   func _physics_process(delta: float) -> void:
       var directionX:float = Input.get_axis("ui_left", "ui_right")
       var directionY:float = Input.get_axis("ui_up", "ui_down")
       velocity.x = directionX * 300.0
       velocity.y = directionY * 300.0
       move_and_slide()

But to simplify our code, we won't Use a different variable for the Y-axis.
Instead, we'll create a variable called ``direction`` which will be a ``Vector2``, with the x-coordinate of ``directionX`` and the y-coordinate of ``directionY``.
Here's the new code for movement along both axes:

.. code-block:: gdscript

   @export var speed:float = 300.0

   func _physics_process(delta: float) -> void:
       var direction:Vector2 = Vector2(Input.get_axis("ui_left", "ui_right"), Input.get_axis("ui_up", "ui_down"))
       velocity = direction * speed
       move_and_slide()

This code works exactly the same way as the previous code, but unlike the previous one,
this one doesn't need to individually assign the values ​​of ``velocity.x`` and ``velocity.y``;
it assigns ``velocity`` directly.
Furthermore, in this code, we'll store the maximum speed in a variable, ``speed``.

.. _anims-fin:

Character Animation
----------------------

Currently, our character moves, but always remains statically within the same frame of the same animation.
It's time to change that!

Starting the animation at the beginning of the game
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, we need the character animation to play as soon as it's added to the game.
To do this, we can use this code:

.. code-block:: gdscript

   func _ready():
       $AnimatedSprite2D.play("idle")

The ``_ready()`` function executes as soon as the object is added to the scene.
Next, the line ``$AnimatedSprite2D.play("idle")`` takes the child ``AnimatedSprite2D`` of our player,
and tells it to play the ``idle`` animation (the default animation).

Dynamic Animation Change
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now that the animation is playing, we'd like it to change dynamically depending on whether the character is moving or not.
To do this, we'll detect, in ``_physics_process``, when the player is moving or not.

You can add this code snippet to the end of ``_physics_process``:

.. code-block:: gdscript

    func _physics_process(delta):
        # ...
        if direction == Vector2.ZERO:
            $AnimatedSprite2D.animation = "idle"
        else:
            $AnimatedSprite2D.animation = "run"

So, with each update, we'll check if the player is stationary (if they're not moving in any direction).
If `yes`, we'll tell ``AnimatedSprite2D`` to change its animation to the ``idle`` animation.
If `no`, it means the player is moving,
so we'll tell ``AnimatedSprite2D`` to change its animation to the ``run`` animation.

Dynamically Changing Sprite Orientation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We have an animated sprite whose animation changes dynamically.
But whether you go right or left, the sprite itself is always facing right.

So we're going to rotate the player's sprite according to the direction the player is moving.

.. hint:: Exercise: Rotate the player according to their direction
   Rotating the player according to where they are going is similar to changing their animation depending on whether they are running.
   Try implementing this functionality on your own, without looking at the solution.
   Hint: By default, ``$AnimatedSprite2D.flip_h = false``, and you need to set this variable
   to ``true`` to flip the sprite.

The code to do this is:

.. code-block:: gdscript

    if direction.x > 0:
        $AnimatedSprite2D.flip_h = false
    elif direction.x < 0:
        $AnimatedSprite2D.flip_h = true

.. warning::
   If in the previous code you had used an ``else:`` instead of ``elif direction.x < 0:``,
   your player will turn around to face their initial direction as soon as you stop moving.

.. _move-fin:

Refining the Movements
-------------------------

Currently, we have a movement system that works,
but it's quite rudimentary, so we're going to improve it!

Adjusting Diagonal Movement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The first problem is that our player moves faster when moving diagonally than when moving in a straight line:

.. image:: img/movementnorm.png

Here we see that the blue vector (diagonally) has a larger norm than the red and green vectors (which are unit vectors, meaning their norm is 1).
Thus, when the character moves diagonally, they move faster:

.. math::
   N_{red} = \left\| \begin{pmatrix} 1 & 0 \end{pmatrix} \right\| = 1 \quad
   N_{green} = \left\| \begin{pmatrix} 0 & 1 \end{pmatrix} \right\| = 1 \quad
   N_{blue} = \left\| \begin{pmatrix} 1 & 1 \end{pmatrix} \right\| = \sqrt{2}

To fix this, we need to ensure that the length of the direction vector is always equal to 1; this is called normalizing a vector.
For this, there is the ``.normalized()`` method which returns the normalized vector.

You can therefore add it to the end of the ``direction`` definition:

.. code-block:: gdscript

   var direction:Vector2 = Vector2(Input.get_axis("ui_left", "ui_right"), Input.get_axis("ui_up", "ui_down")).normalized()

Adding Inertia
~~~~~~~~~~~~~~~

Currently, our player reaches their maximum speed instantly and stops instantly.

To remedy this problem, we will use a function called ``lerp``, which is used as follows:

.. code-block:: gdscript

   val = lerp(val, max_val, poids)

It will return the next value our variable should take,
to ensure a smooth transition between the initial value and our maximum value.
The weight will allow us toTo determine the "smoothness" of the transition:

.. image:: img/graphLerp.png

In our case, the weight will represent the acceleration.
However, we want it to depend on the elapsed time,
and not on the number of frames (because the number of frames per second can vary depending on the computer).

We can therefore initialize a variable ``acceleration`` in the main body:

.. code-block:: gdscript

   @export var acceleration:float = 10

And change the line that assigned a value to ``velocity`` in ``_physics_process(delta):``:

.. code-block:: gdscript

   velocity = lerp(velocity, direction * speed, acceleration * delta)

And with that, we have finished creating our player, as well as its movement system!
