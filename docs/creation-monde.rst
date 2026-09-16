World Creation
=================

Initializing the World
-----------------------

Currently, we have a player, but we don't have the world in which this player will move.
To create this, we'll start by creating a new scene, which will be our `World`.

In this section, we'll create everything you see in the image below.
Namely, the grass and the walls, which will have collision detection so the player cannot pass through them.

.. image:: img/emptyworld.png

Click on **Scene -> New Scene** in the top right corner, or on the small **+** at the top next to the scene's ``player`` tab, or press ``Ctrl+N``.
A new blank scene should open:

.. image:: img/worldCreation.png

.. hint:: If you've stayed in the code editor, you can return to the 2D editor by clicking the ``2D`` button at the top of the window.

Here, we'll create a ``Node2D``. To do this, click ``2D Scene`` in the hierarchy (top left).
You can rename this node to ``World`` and add a ``TileMapLayer`` node as a child.

.. warning::
   Since Godot version 4.3, the ``TileMap`` node, which was used until then, is now obsolete! The functionality is generally similar, but be sure to use a ``TileMapLayer`` node.

.. .. note::: 
   A tilemap divides the world into a grid. The cells of this grid are filled with blocks that you place to build the world.
   This technique is very common in 2D games. If you've played Mario Maker, you know that when you create a level, you're essentially manipulating a tilemap.

It involves creating the world by gluing small blocks of terrain, called `tiles`, together.
This not only simplifies level creation but also optimizes the game.

Customizing the TileMapLayer
-----------------------------

We've just created a ``TileMapLayer``, but it doesn't yet contain any `tiles` to place in our world.
For that, we'll create a ``TileSet``.

.. note:: 
   A tileset is a bit like a palette in painting.
   This is where all the blocks we'll use to "paint" our world will be stored.
   The tileset contains not only visual information (what the block looks like), but also other information such as block collision details.

To add a ``TileSet`` to the ``TileMapLayer``, click **Tileset -> New Tileset** in the Inspector.
The **TileSet** and **TileMap** tabs should then open in the bottom window of the editor.
Click the **TileSet** tab:

.. image:: img/tilesetEmpty.png

Press the **+** **[1]** button, click **Atlas**, and then select the file ``assets/tilemap/Tilemap_Flat.png``.
Godot will then ask if you want to automatically create tiles in the Atlas. 
Select yes, and you'll see a grid divide the image into 16px by 16px blocks.
However, we want 32px by 32px tiles (the size depends on your tileset, but this one was designed for 32x32 tiles).

.. image:: img/tilesetGridUncorrectSize.png

To fix this, you need to change the size of the `tiles` from ``16px`` to ``32px``,
both in the ``TileMapLayer`` **[1]** and in the ``TileSet`` **[2]**.

.. image:: img/tilesetTilesSizeChange.png

Now that you've created your tileset, you can go to the **TileMap** tab to "paint" the world.
To do this, simply click on the block you want to place and "paint" your world in the editor.

For a faster approach, you can select the large square of grass and use the **Rectangle** tool to directly "paint" a large rectangle of grass.
You should get a result similar to this:

.. image:: img/projectaftergrass.png

You'll notice that the tilemap grid doesn't quite align with the window (the slightly purple rectangle in the editor).
To fix this, we'll resize the window to a multiple of 32 (the size of the tiles we're using).
Go to **Project -> Project Settings**. Then, under **Display**, click on **Windows** and change:

- **Viewport Height** = 640
- **Mode**: ``canvas_item``

.. image:: img/projectsettingswindow.png

Creating Walls
-----------------

Now we can move on to the walls. To do this, create a new ``TileMapLayer`` that you will call ``"TileMapLayerWalls"``, for example.
Add a new ``TileSet`` in the Inspector, and change the tile size to ``32px``.

We want our walls to have collisions. To do this, under the **Physics layers** tab of the ``TileSet``, click the **Add Element** button.
This will add a new ``Physics layer``. If you want to learn more about how they work exactly, you can click `here <https://docs.godotengine.org/en/stable/tutorials/physics/physics_introduction.html>`_.

.. image:: img/newphysicslayer.png

In the **TileSet** tabNext, add a new Atlas, as before, this time with the texture ``assets/tilemap/Tilemap_Elevation.png``, and click Yes in the popup that appears.
The tiles we have here don't yet have collision detection.

To do this, go to the **Paint** tab and select the ``Physics Layer 0`` property.

.. image:: img/paintproperty.png

The **Paint** tab is used to add properties to the tiles we use.
Here, we'll add the property of belonging to Physics Layer 0, and therefore have collision detection.
After selecting the property, click on all the tiles to the right.
Clicking on a tile paints the ``"Physics Layer 0"`` property onto it (hence the name of the **Paint** tab). 
The tiles should turn blue, meaning you've just added a hitbox to them. You can click and drag the mouse to move faster.

Once you're sure all the tiles have a hitbox, you can paint them from the **TileMap** tab, as before.
Try to reproduce the result below:

.. image:: img/emptyworld.png

Adding the player
---------------

You've finished the world! Add your player by clicking on **Instantiate Child Scene** (the chain icon), or by pressing ``Ctrl+Shift+A``:

.. image:: img/addplayer.png

Make sure the player is placed **below** the ``TileMapLayers`` in the Scene Tree so that they are visible **above** the in-game tiles.
Also check that the player cannot pass through walls, and you're good to go!
