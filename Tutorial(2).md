# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 2. Create a Scripts called Player

Create a folder called Scripts right click and you see create hover over it and go to C# script then change the name to Player drag it onto your player character.

Double click on the script and wait for it to open.

We going to make the Player be able to Jump over the obstacles in this Script.

First we make a two private variable one called "CharacterController character and the other called Vector3 direction.

We will need a variable to allow us to modify the character's position which is the vector3 direction.

We can use a reference to the player's character controller component for that. 


,,,
    
    private float CharacterController character
    
    private Vector3 direction; 

,,,

Now add two public float called gravity and give a value of 9.81f and times it by two and the other is jumpForce 8f. 
The gravity is is roughly close to real life gravity then adjust to how you want it in the game.

The gravity stops the character for flying out endless into the sky and the jumpforce is allow the character to jump big or small.
,,,

    { public float gravity = 9.81f * 2f;
      public float jumpForce = 8f;
    }
    

,,,

We going to add a private void called Awake. Which we add character get component CharacterController

The Awake function allows us to do something before the game actual starts up. The get component is letting the character(Us) control the player.
,,,

    private void Awake()

    {
      character = GetComponent<CharacterController>();
    }

,,,

After this we add another private void called OnEnable then we add direction variable.

On Enable function allows us to control when we won't something in our game or not it check weither it on if not it turns it self on.

,,,
   
    private void OnEnable() 
    {
      direction = Vector3.zero;
    }

,,,

Then go to void Update so we join our variables together.

This code is basically saying if you press the space button to jump the gravity pressure will stop you from jumping too high.

Void Update is a function that continually runs until we turn off the game.

Vector 3 allows us to move in the x,y and z axis(Up,Down,Left and Right).

Time deltaTime is a function that allows the all computer to run with a certain amount of frames per minute.

Input GetButton is when we press the button specified it then does it.

If statement are if I do this then work if not don't do it.

So by connecting these together we allow the character to move in any direction that fits our game purpose.

In this tutorial we moving the character up and the gravity brings it down. Code shown below.

,,,

    private void Update()
    {
        direction += Vector3.down * gravity * Time.deltaTime;

        if (character.isGrounded) 
        {
            direction = Vector3.down;
            if (Input.GetButton("Jump"))
            {
                direction = Vector3.up * jumpForce; 
            }

        }

        character.Move(direction * Time.deltaTime);
    }


,,,