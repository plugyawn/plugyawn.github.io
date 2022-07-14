---
layout: default
---

## Two Opposites
Two opposites is a game about the journey of two opposites (characters with mirrored controls) separated by a mirror. They need to solve puzzles to escape the mirror world and finally meet each other. However, the challenge lies in the fact that they can only solve these puzzles together. You can play it in your browser [here](https://makra.itch.io/two-opposites) <br><br>
The game was made in a week (in a team of three) for the Brackeys Game Jam (10k+ people participated worldwide) and ranked **#22 in the innovation category.** <br>

<a href="../files/TwoOppLogo.png" data-lightbox="twoOpposites" data-title="Two Opposites"><img src="../files/TwoOppLogo.png" style="width:100%"></a>

### 1.0 2D Lighting System
Upon initial analysis, we decided that the atmosphere should be given the most priority while developing this game. And the visual appeal of the game played a significant role in that. Back when we started working on this project, Unity didn't have any rendering pipeline that supported 2D lighting. So my task was to develop a 2D lighting system for the game.

### 1.1 2D Raycaster (GL) - 1st iteration
* The basic idea was to draw transparent lines originating radially outwards from a sprite with negligible separation to give a sense of light coming out.
* I used the Unity's low level [Graphics Library (gl)](https://docs.unity3d.com/ScriptReference/GL.html) to draw lines between two points.
* The raycast loop formulated- <br>

<a href="../files/raycast_loop.png" data-lightbox="raycastloop" data-title="Raycast Loop"><img src="../files/raycast_loop.png" style="width:100%"></a> <br><br>

* This loop draws rays from the player's position to equally spaced points around the player.
* The angle that light covers is governed by **theta**.
* The spacing between each ray is governed by **steps**.
* The color of the rays is governed by **col**.
* The length of light ray is governed by **maxVisiblityDistance**.
* All of these variables were serialized in the inspector.
* This script is attached to the MainCamera and the loop is called in **OnPostRender()** method so that the lines are rendered as soon as the camera finishes rendering the scene.

<table border="0">
 <tr>
    <td><a href="../files/theta.gif" data-lightbox="parameters" data-title="Adjusting theta"><img src="../files/theta.gif" style="width:100%"></a></td>
    <td><a href="../files/steps.gif" data-lightbox="parameters" data-title="Adjusting steps"><img src="../files/steps.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Adjusting theta</td>
    <td>Adjusting steps</td>
 </tr>
</table>

<table border="0">
 <tr>
    <td><a href="../files/col.gif" data-lightbox="parameters" data-title="Adjusting color"><img src="../files/col.gif" style="width:100%"></a></td>
    <td><a href="../files/maxvdist.gif" data-lightbox="parameters" data-title="Adjusting max visibility distance"><img src="../files/maxvdist.gif" style="width:100%"></a></td>    
 </tr>
 <tr>
    <td>Adjusting color</td>
    <td>Adjusting max visibility distance</td>
 </tr>
</table>

### 1.2 Ray Material
* The next task to make the light rays feel more natural by introducing transparency.
* While pondering I found that GL library by default uses the Unlit material provided by Unity to create the lines.
* As the Unlit Material doesn't support transparency by default, I wrote an Unlit Shader that supported both transparency and vertex colors.
* The RGBA values of the colors of the material based upon this shader was passed as an input. <br>

<a href="../files/RGBA.png" data-lightbox="rgba" data-title="RGBA Input"><img src="../files/RGBA.png" style="width:100%"></a>

* With transparency controls, the rays looked more natural. <br>

<a href="../files/TRays.gif" data-lightbox="rgba" data-title="Light looks more natural"><img src="../files/TRays.gif" style="width:100%"></a>

### 1.3 Environment Lighting
* The next step would be to make the scene react to the light rays emitted by the player.
* This involved two steps-

1. Making the light ray stop when it hits an object. This is done by Raycasting along the light rays that GL draws and checking if we've hit something. <br>
<a href="../files/RaycastHit.png" data-lightbox="envlight" data-title="Stopping if we hit something"><img src="../files/RaycastHit.png" style="width:100%"></a>
2. Making the sprite color of the object depend upon its distance from the light source. <br>
<a href="../files/spritecol.png" data-lightbox="envlight" data-title="Sprite color dependent on distance from light source"><img src="../files/spritecol.png" style="width:100%"></a>

### 1.4 Final Output
<a href="../files/2dlightsys.gif" data-lightbox="finalenvlight" data-title="Natural Light with dynamic environment reacting to it"><img src="../files/2dlightsys.gif" style="width:100%"></a>

### 1.5 2D Raycaster (GL) - 2nd iteration
* The previous method for generating rays was very inefficient with time complexity of O(n) as the loop had to run 3600 times every frame with a step size of 0.1.
* This issue was solved by detecting the edges of nearby objects and casting rays at them and then filling the space by generating mesh between them. <br><br>
<a href="../files/mesh2dlight.png" data-lightbox="mesh2dlight" data-title="Detecting the edges of nearby objects and generating mesh between them."><img src="../files/mesh2dlight.png" style="width:100%"></a>

### 1.6 Final Output
<a href="../files/2dmeshlightsys.gif" data-lightbox="finalmesh2dlight" data-title="Looks exactly like individual rays"><img src="../files/2dmeshlightsys.gif" style="width:100%"></a>

### 2.0 Environment Reflection
* Two players (each with their own top down camera) were added in either sides of the map separated by a box collider.
* The screen was split into two (one for each camera) by decreasing the width of the both camera's viewport rect to 0.5 and offsetting one of them to 0.5.

### 3.0 Player Movement 
* A simple rigidbody top down controller was yoinked from one of Brackeys tutorials for the first player while the movement of the second player was made to be governed by that of the first player's. <br><br>
<a href="../files/inversion.png" data-lightbox="inversion" data-title="Movement Lateral Inversion"><img src="../files/inversion.png" style="width:100%"></a>
* This inverts the movement of the second player horizontally (lateral inversion) as if their movements were mirrored.
<a href="../files/inversion.gif" data-lightbox="inversion" data-title="Output on inverted movement."><img src="../files/inversion.gif" style="width:100%"></a>

### 3.1 Player Sprites & Animations
* Two sprite sheets of the top-down view of a male & female character (drawn by one of my teammates) walking were imported into the game. 
* These sprites were split into frames for animation using Unity's inbuilt sprite editor.

<table border="0">
 <tr>
    <td><a href="../files/BoySprite.png" data-lightbox="ss" data-title="Boy Sprite Sheet"><img src="../files/BoySprite.png" style="width:100%"></a></td>
    <td><a href="../files/GirlSprite.png" data-lightbox="ss" data-title="Girl Sprite Sheet"><img src="../files/GirlSprite.png" style="width:100%"></a></td>    
 </tr>
 <tr>
    <td>Boy Sprite Sheet</td>
    <td>Girl Sprite Sheet</td>
 </tr>
</table>

* These were animated at 10 fps.
* The controller was tweaked to support both animation and smooth rotation of the player sprites.
<a href="../files/newmov.png" data-lightbox="newmov" data-title="New Player Controller"><img src="../files/newmov.png" style="width:100%"></a>

* The translation is governed by Unity's Physics engine (using rigidbodies) and is executed in the **FixedUpdate()** method to keep it independent of frame rate.
* The rotation of the sprite changes with its direction (governed by the combination of vertical and horizontal input).
* The translation and rotation speed is parametrically controlled by **speed** and **rotSpeed** variable exposed in the inspector.
* The animation is simply enabled if we're sending an input, else it stays disabled. <br><br> 
<a href="../files/Sprites.gif" data-lightbox="newmovoutput" data-title="New Player Movement with Animations"><img src="../files/Sprites.gif" style="width:100%"></a>

### 4.0 Button Mechanic
We decided to come up with a button mechanic system. The idea was to spawn two buttons (one in each world) and the player was expected to walk over both the buttons simultaneously to open the gates so that he can people can proceed to the next level.
* When the player walked over a button, the button's sprite renderer glowed.
* Also, an event was called to check if the other button is pressed as well.
* If the other button was pressed, the gates (which were hinged at their corner) would rotate and the player could pass through them. <br><br>
<a href="../files/Buttons.gif" data-lightbox="btn" data-title="Button Mechanic"><img src="../files/Buttons.gif" style="width:100%"></a>

### 5.0 Movable Objects
To add more depth to the puzzles, we decided to come up with a few objects that the players could push in order to block or press something. 
* A physics material (with high coefficient of friction value & 0 bounciness) is created.
* Sprites for movable objects (with hand-drawn texture maps by one of the teammates) are imported.

<table border="0">
 <tr>
    <td><a href="../files/crate.png" data-lightbox="crate" data-title="Crate base map"><img src="../files/crate.png" style="width:100%"></a></td>
    <td><a href="../files/cratenormal.jpg" data-lightbox="crate" data-title="Crate normal map"><img src="../files/cratenormal.jpg" style="width:100%"></a></td>    
 </tr>
 <tr>
    <td>Crate base map</td>
    <td>Crate normal map</td>
 </tr>
</table>

* These textures are assigned to the URP's default lit sprite material.
* Their prefabs are created with Box Collider 2D & Rigidbody 2D components having the physics material assigned to them. <br><br>
<a href="../files/Pushable.gif" data-lightbox="pushable" data-title="Pushable Objects"><img src="../files/Pushable.gif" style="width:100%"></a>

### 6.0 Death Mechanic
We decided to include spikes in the game. They would kill the players on contact, rendering few areas of the game as unapproachable. The death animations and effect were kept as brutal and gross (taking inspiration from Limbo) to add to the dark atmosphere of the game.

* Colliders were set up on the spikes (with 'Death' tag) and the player.
* If the player comes in contact with the spike a Coroutine containing all the relevant methods for death of the player is called.

<a href="../files/death2opp.png" data-lightbox="death" data-title="Death Logic"><img src="../files/death2opp.png" style="width:100%"></a>

### 6.1 Spike Texture
* Since our core idea was to make the game atmospheric & appealing to eyes we wanted to keep environment ques pretty detailed. We decided to do the same with the spikes.
* The spike texture maps were hand-drawn by one of the teammates. We had initially thought of including a height/bump map but later replaced it with a normal map.

<table border="0">
 <tr>
    <td><a href="../files/spikes.png" data-lightbox="spike" data-title="Spike base map"><img src="../files/spikes.png" style="width:100%"></a></td>
    <td><a href="../files/SpikesNormal.png" data-lightbox="spike" data-title="Spike normal map"><img src="../files/SpikesNormal.png" style="width:100%"></a></td>
    <td><a href="../files/spike height.png" data-lightbox="spike" data-title="Spike height map"><img src="../files/spike height.png" style="width:100%"></a></td>    
 </tr>
 <tr>
    <td>Spike base map</td>
    <td>Spike normal map</td>
    <td>Spike height map</td>
 </tr>
</table>

* These textures are assigned to the URP's default lit sprite material.

### 6.2 Death Animation
* A sprite sheet for hand-drawn animation of blood splash was imported.

<a href="../files/BloodSplash.png" data-lightbox="bloodsplash" data-title="Blood Splash sprite sheet"><img src="../files/BloodSplash.png" style="width:100%"></a>

* This sprite sheet was played on collision with the spikes.
* The movement state of the players were changed from animated to static.
* The movement vector of the players were overridden to be zero.
* The canvas was fade out to black and the level was reloaded.

<a href="../files/death2oppcor.png" data-lightbox="deathlogic" data-title="Death Coroutine"><img src="../files/death2oppcor.png" style="width:100%"></a>

### 6.3 Final Ouptut
<a href="../files/death2opp.gif" data-lightbox="deathoutput" data-title="Death"><img src="../files/death2opp.gif" style="width:100%"></a>

### 7.0 Level Design
The biggest challenge ahead of us was actually to come up with a level design that would keep the people engaged till the end of the game and not feel tiring at the same time (Since atmospheric games heavily rely on the level design). As the game was a submission to a gamejam we decided to keep the total play time around 10-15 minutes.

### 7.1 Initial levels
* The key concept of an accessible game design is to keep the initial levels of the game feel more like tutorials that help people stumble upon the core mechanics and gameplay features that game has to offer.
* The challenge with atmospheric though is that they can't give away much visual cues about the game, the player is expected to explore and find it himself. But again, the game was a part of a game jam submission wherein the attention span of the players playing the game is quite small, so keeping things extremely vague might lead to less player retention. So we decided a sweet spot in between them.
* The game started with a WSAD key sprite I made using Adobe XD fading into the scene giving the player idea of the controls.

<table border="0">
 <tr>
    <td><a href="../files/WSADGame.png" data-lightbox="WSAD" data-title="WSAD Key Sprite in Game"><img src="../files/WSADGame.png" style="width:100%"></a></td>
    <td><a href="../files/WSADXD.png" data-lightbox="WSAD" data-title="WSAD Key Sprite made in Adobe XD"><img src="../files/WSADXD.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>WSAD Key Sprite in Game</td>
    <td>WSAD Key Sprite made in Adobe XD</td>
 </tr>
</table>

* An arrow sprite was made using Photoshop which was spawned in the game's first level to guide directions to the gate that next level. These arrows were spawned if the player exceeded a certain threshold time to reach the gates. 

<table border="0">
 <tr>
    <td><a href="../files/ArrowGame.png" data-lightbox="Arrow" data-title="Arrow Sprite in Game"><img src="../files/ArrowGame.png" style="width:100%"></a></td>
    <td><a href="../files/ArrowPS.png" data-lightbox="Arrow" data-title="Arrow Sprite made in Photoshop"><img src="../files/ArrowPS.png" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Arrow Sprite in Game</td>
    <td>Arrow Sprite made in Photoshop</td>
 </tr>
</table>

* This level was kept simple and most importantly symmetric. The players were just expected to roam around, get familiar with the inversion mechanic and the gates that would progress them to the next level. <br><br>
<a href="../files/Lev1.png" data-lightbox="level" data-title="1st Level"><img src="../files/Lev1.png" style="width:100%"></a>

* The first challenge was introduced in the next level as the it was kept asymmetric. Now players needed to figure out a way to make both the characters back in sync with each other so that they reach the gates. <br><br>
<a href="../files/Lev2.png" data-lightbox="level" data-title="2nd Level"><img src="../files/Lev2.png" style="width:100%"></a>

* The third level introduced the button mechanic in the game. The gates are kept locked and the players are expected to align both the characters over the button simultaneously to unlock the game. The player would use the same method he used to sync both the characters in the previous level as the outline of both the levels is kept the same. <br><br>
<a href="../files/Lev3.png" data-lightbox="level" data-title="3rd Level"><img src="../files/Lev3.png" style="width:100%"></a>

### 7.2 Later Levels
* The difficulty for the game was now gradually increased and the game now focused more on the player creatively finding out a way to solve the puzzles rather than teaching the player how to play.
* For the next level, the the button for one of the characters was spawned right next to him. Our solution to this was locking one of the players in the slots next to the button while the other traveled to his button. To our surprise the players came up with various other solutions to this puzzle too (This is true in the case of the subsequent levels as well). <br><br>
<a href="../files/Lev4.png" data-lightbox="level" data-title="4th Level"><img src="../files/Lev4.png" style="width:100%"></a>

* The next level had both the puzzles on different vertical levels but symmetric to each other. <br><br>
<a href="../files/Lev5.png" data-lightbox="level" data-title="5th Level"><img src="../files/Lev5.png" style="width:100%"></a>

* Now that the player knew how to sync the characters and solve the puzzles in both vertical and horizontal directions, it was now the time to introduce the spikes into the level. So the next was similar to the previous one except for the addition of spikes on some of the walls. This limited the areas that the player could explore to solve the puzzle. <br><br>
<a href="../files/Lev6.png" data-lightbox="level" data-title="6th Level"><img src="../files/Lev6.png" style="width:100%"></a> 

* The next level drastically increased the difficulty of the game by introducing a maze like map with the buttons at the end of the maze and spikes on a few of the walls. Lots of players exclaimed about getting stuck on this level. <br><br>
<a href="../files/Lev7.png" data-lightbox="level" data-title="7th Level"><img src="../files/Lev7.png" style="width:100%"></a> 

* Now the players were introduced to the movable boxes that were to be strategically used to solve the puzzles. <br><br>
<a href="../files/Lev8.png" data-lightbox="level" data-title="8th Level"><img src="../files/Lev8.png" style="width:100%"></a> 

* The next few levels combined the usage of both box and spikes along with maze-like level designs. <br><br>
<a href="../files/Lev9.png" data-lightbox="level" data-title="9th Level"><img src="../files/Lev9.png" style="width:100%"></a> 

* The final level involved a cliffhanger ending followed by the credit screen. Play the game to know more ;) <br><br>
<a href="../files/LevFin.png" data-lightbox="level" data-title="Final Level"><img src="../files/LevFin.png" style="width:100%"></a> 

### 8.0 Post Processing  
We used post processing to increase the immersion that the game offers. We decided to limit ourselves to the stack that were well optimized for WebGL builds. 
* Lens distortion and Chromatic Aberration were added to the images rendered by the camera a more natural. This causes the shape of the images rendered by the camera to distort at the edges and thus increase the focus of the environment in proximity of both the players.
* We had planned on adding Bloom as well but since we weren't Unity's lighting system we would have to write the Bloom system for our lighting system. Due to deadlines for the gamejam approaching, we decided to shelve the idea. <br><br>
<a href="../files/PP.gif" data-lightbox="PP" data-title="Post Processing"><img src="../files/PP.gif" style="width:100%"></a>

### 9.0 Game UI & UX
For UI, we decided to keep it minimal and match the atmospheric tone of the game. 

### 9.1 Font
* We browsed through a bunch of hand-drawn fonts for the game's UI. 
* We shortlisted to Architects Daughter, Amatic, and Blokletters and finally finalized Amatic. 
* The color palette was kept limited and preferably lerped between black and white. <br><br>
<a href="../files/amatic.png" data-lightbox="font" data-title="Amatic font"><img src="../files/amatic.png" style="width:100%"></a>

### 9.2 Animations
* The animations were kept minimal - fading, scaling, and translations. 
* A canvas with black panel was used as an overlay and it was used for fading transitions between different scenes and menus.

<table border="0">
 <tr>
    <td><a href="../files/menuanim.gif" data-lightbox="menuanim" data-title="Main Menu"><img src="../files/menuanim.gif" style="width:100%"></a></td>
    <td><a href="../files/pausemenu.gif" data-lightbox="menuanim" data-title="Pause Menu"><img src="../files/pausemenu.gif" style="width:100%"></a></td>
 </tr>
 <tr>
    <td>Main Menu</td>
    <td>Pause Menu</td>
 </tr>
</table>

### 9.3 Intro clip
We created a small clip using Unity's timeline as with the text only, the menu seemed a little lifeless. Again, minimalism and dark atmosphere were the key. <br>

<a href="../files/mainmenu.gif" data-lightbox="mm" data-title="Main Menu Final"><img src="../files/mainmenu.gif" style="width:100%"></a>

### 9.4 Music & Sound Effects
* Simple sound effects imported from [ZapSplat](https://www.zapsplat.com/) were used to for clicks, death, button press, gates and various other purposes.
* A [free for profit sad piano beat](https://www.youtube.com/watch?v=E3yKY6D7j_M) by Loud Jezze was used as the background track.
* Drawing cues from Minecraft, the soundtrack was played whenever the game became intense.
* The soundtrack was played one of four timestamps so that it doesn't feel repetitive. 
* Also, with each scene, the soundtrack's instance was destroyed if it was already playing to avoid multiple instances.
* The soundtracks were muffled in the menus.