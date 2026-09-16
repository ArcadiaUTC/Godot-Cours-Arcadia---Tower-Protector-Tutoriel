Discovering Godot
===================

In this part of the tutorial, we'll install Godot and create our project.

What is Godot?
------------------

The Godot Engine is a free and open-source game engine that's very easy to use.
Godot allows you to develop 2D and 3D games thanks to an intuitive visual interface and an easy-to-learn scripting language, `GDScript <https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html>`_, which is very similar to Python.
Godot is used for small indie games (like ours!) as well as more complex games (like ours in the future, we hope!). Examples include `Dome Keeper <https://godotengine.org/showcase/dome-keeper/>`_ and `PVKK <https://godotengine.org/showcase/planetenverteidigungskanonenkommandant/>`_ from the studio `Bippinbits <https://bippinbits.com/>`_.

Godot works with scenes and nodes. We'll come back to this later, but a node is a basic element that makes up your scenes.
You can make your scenes interact with each other (for example, putting the *Player* scene inside the *World* scene).


.. installating-godot:

Installing Godot
---------------------

To begin the tutorial, you will need to install Godot. To do this, you can go to `this site <https://godotengine.org/download/>`_ to download the latest version of Godot.

.. note::
   This tutorial was written for Godot 4.3. It shouldn't change much for future versions, but if you see a problem, let us know!

Once the .zip file is downloaded and unzipped, you can launch the installer, and after a short wait, you will be able to launch Godot and be greeted by this window:

.. image:: img/projectmanager.png


Creating your first project
--------------------------------

This window is called the **Project Manager**. This is where you will find your different projects once you have created them.
Currently, the **Project Manager** is empty, so let's create our first project.

.. note:: 
   It's generally better to use English for everything when programming, as online documentation is usually more comprehensive in English than in othe languages.
   You are free to set your editor to the language of your choice, but some buttons may not have the same labels on your system.
   You can change the editor language in the **Settings** in the top right corner of the **Project Manager**, or in **Editor Settings** within the editor itself.

Click the **Create** button in the top left corner to create a new project.
A pop-up window will open, asking you for information about your project. Name your project ``"Arcadia Tutorial"`` **[1]**, and choose the folder where you want it stored **[2]**.

.. image:: img/newproject.png

Leave the other settings as they are for now, and create your project. A new window should open.
This is the main Godot window, the editor, where you'll do everything on your games.

The Editor
---------

In this section, we'll describe the different elements that make up the editor:

.. image:: img/fulleditor.png

1. In the middle, you'll find the main editor window, which allows you to view and modify the different scenes of your project.

2. In the bottom left, you'll find the **Project Tree**.
   This is actually the folder you just created when creating the project.
   You can find it on your computer by following the path to your project (which you filled in earlier) or by **Right-clicking -> Open in File Manager**.

3. Just above, in the top left corner, you'll find the **Scene Tree**. This is where you can modify the current **scene**.
   Each part of the game (the player, the enemies, the world) is a scene.
   A scene is composed of a **root** node, which can have several child nodes.
   Each node has a specific role (one node for collision, one for textures, etc.). We'll learn more about how this works when we create the player. Since a scene is simply a parent node and its children, it's entirely possible to make an entire scene a child of another scene.

4. On the right, you can see the **Inspector**. This is the part of the editor that allows you to modify the various parameters of the selected node.
   It's currently empty (which is normal since there are no nodes selected), but we'll be using it very often.

5. At the top, you'll find the different tabs. Currently, you should be on the **3D** tab, which is used to view 3D scenes.
   We won't be using it for this project, which will be entirely 2D (so we'll use the **2D** tab).
   There's also the **Script** tab, which is where we'll write all our code.
   And the **AssetLib** tab, which we won't use for now, but where you can download assets created by other people.

6. In the top left, you'll find various settings.
   The most important tab is **Project -> Project Settings**, where you can modify the various project settings (like the window size, for example).

7. In the top right corner, you'll find various buttons to launch your project. Here are the three most important:
   * **Triangle** *(F5):* Launch the project (launches the game from the title screen, just like a player would).
   * **Square** *(F8):* Stop the project while it's running (very useful!).
   * **Clap with a small triangle** *(F6):* Launch the current scene, very useful when you want to debug a scene without having to restart the entire game each time to access it.

8. And at the bottom, you'll find the rest of the editors. Everything that isn't in the other sections is at the bottom.
   This includes, for example, the debug window, the animation editor, and the tilemap editor. We'll come back to these later, especially when we discuss player animations.

Importing Assets
-------------------

After creating the project, we need to install the various `assets` we will use for this tutorial.

.. note:: 
   An `asset` is the name given to the elements of a video game (generally non-code). For example, a texture, a sound, and a font are assets (respectively visual, audio, and re-visual).

To do this, download the file :download:`here <resources/Godot-Cours-Arcadia---Tower-Protector--- Assets.zip>`, extract the ``assets`` folder, and place it in your project folder.
Your project folder should contain at least the following:

.. image:: img/filesAsset.png

Once this step is complete, we can start creating our first game! Click the *Next* button to continue this tutorial!
