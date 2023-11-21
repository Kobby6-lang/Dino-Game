# Dino Game Tutorial

I used this code from https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 2. Create a Script called Player

Create a folder called Scripts. right-click, and you will see Create. Hover over it and go to the C# script. Then change the name to Player and drag it onto your player character.

Double-click on the script and wait for it to open.

We are going to make the Player be able to Jump over the obstacles in this Script.

First, we make two private variables, one called "The CharacterController character and the other called Vector3 direction.

We will need a variable to modify the character's position, the vector3 direction.

We can reference the player's character controller component for that. 


,,,
    
    private float CharacterController character
    
    private Vector3 direction; 

,,,

Now add two public floats called gravity, giving a value of 9.81f and times it by two; the other is jump force 8f. 
The gravity is roughly close to natural life gravity, then adjust to how you want it in the game.

The gravity stops the character from flying out endlessly into the sky, and the jumpforce allows the character to jump big or small.
,,,

    { public float gravity = 9.81f * 2f;
      public float jumpForce = 8f;
    }
    

,,,

We are going to add a private void called Awake. We add character get component CharacterController.

The Awake function allows us to do something before the game starts. The get component is letting the character(Us) control the player.
,,,

    private void Awake()

    {
      character = GetComponent<Charactesee rController>();
    }

,,,

After it checks whether  p. Ifate, void called OnEnable, we add a direction variable.

On Enable function allows us to control when we don't see something in our game or not it check weither it on if not it turns it self on.

,,,
   
    private void OnEnable() 
    {
      direction = Vector3.zero;
    }

,,,

Then go to void Update so we join our variables together.

This code says that if you press the space button to jump, the gravity pressure will stop you from jumping too high.

Void Update is a function that continually runs until we turn off the game.

Vector 3 allows us to move in the x,y and z axes (Up, Down, Left and Right).

Time deltaTime is a function that allows all computers to run with a certain number of frames per minute.

Input GetButton is when we press the button specified it then does it.

If the statement is If I do this, then work if not don't do it.

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
