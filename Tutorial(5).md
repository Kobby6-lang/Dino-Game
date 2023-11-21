# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 5.Animated Sprites

Create a C# script called "AnimatedSprite"

Then add in a public spite with an array bracket named sprites and private sprite renderer named spriteRenderer

An array is like a check list for items or objects.

Sprite renderer allows to add in our sprites we made.

The code below is saying a public sprite with an array saying allow you to add in the sprites animation

Calling the sprite renderer so it all works.
,,,

    public Sprite[] sprites;
    private spriteRenderer spriteRenderer

,,,

Add in a private void Awake and inside the brackets add in sprite Renderer get the components of the spriteRenderer variable.

The code is basically saying that sprite renderer is getting the Sprite Renderer of the sprites that have been made.

,,,

    private void Awake() 
    {
       spriteRenderer = GetComponents<SpriteRenderer>()
    }
,,,

Add a private Integer called frame.
,,,

    private int frame;

,,,

Make a private void called OnEnable and Animate.

Add in frame ++ to yanimate to increase the frame rate. 

Then add in if statement saying check if the frame is greater or equal to sprites length then return to zero and start again. 

Then Add in another if statement making sure that the frame will stay in bounds of the array.

 Once animate has be called inkoke the animate by 1 sec / game manager instance game speed.

 Add in invoke name of Animate 0 sec to call this function after the game manager void start.

 Add in private void called OnDisable to get rid of the animation when not in use.

 The code is simple saying that when animation enabled start up the animation when not in use stop animating. 

 This need to be able to allow the character to be have an animation and then stop animation when not in use.

 void animate is calling the animation so it works when you start the game.

 void On disable is when you enable something but you don't want it appearing anymore in your game so the system disable it for you.

 invoke means start something up in this case every o or 1 sec depending on the situations.
 ,,,

    private void OnEnable()
    {
        Invoke(nameof(Animate), 0f);
    }

    private void OnDisable()
    {
        CancelInvoke();
    }

    private void Animate()
    {
        frame++;

        if ( frame <= sprites.Length ) 
        {
            frame = 0;
        }
        if ( frame <= 0 && frame < sprites.Length) 
        {
            spriteRenderer.sprite = sprites[frame];
        }

        Invoke(nameof(Animate), 1f / GameManager.Instance.gameSpeed); 
        }
,,,

 After you finish this add the script to the player and go to the sprites section in the animated sprites script and click on the plus sign and add in you running animations.




 
