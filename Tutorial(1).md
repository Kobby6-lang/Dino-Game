# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 1.Create a new scene

Start by creating a new scene called Dino and delete the original and save it.

Add your sprites that you either got from the net or created it youself put in the assets.

Then click on all the sprites on the right hand side you will see "Wrap mode" change it from** "Clamp"** to **"Repeat"** and **"Filter mode"** change it to **point(no filter)**. 

Wrap mode is determines how time is treated outside of the keyframed range of an AnimationClip or AnimationCurve.
Filter mode is changing the filter of your pixel arts depending on you game.

Still selected unclick the ground sprite and change the under the **Default:Max size:** 2048 to 256 and the ground spite to 4096 then click apply. 

Default mode is the max size of your pixel arts.

After that drag the player sprite in idle position and ground sprites onto the "Hierarchy" click on player go down to add components add in "Character Controller" and if you like change the name of the character to Player or something else.

Character controller allows you the player to be able to control the movements of the player.

Underneath you find "Tag" change it to **"Player"** to let the game know this the character your moving or controlling. 

Then go on ground and add a "Box collider".

A box collider is a collider that makes the game recognize that you crashed into something.

A tag in unity means giving a label to something then calling it later on in the script.