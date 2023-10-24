# Dino Game Tutorial

## 1.Create a new scene

Start by creating a new scene called Dino and delete the original and save it.

Add your sprites that you either got from the net or created it youself put in the assets.

Then click on all the sprites on the right hand side you will see "Wrap mode" change it from** "Clamp"** to **"Repeat"** and **"Filter mode"** change it to **point(no filter)**. 

Still selected unclick the ground sprite and change the under the **Default:Max size:** 2048 to 256 and the ground spite to 4096 then click apply. 

After that drag the player in idle position and ground sprites onto the "Hierarchy" click on player go down to add components add in "Character Controller" and if you like change the name of the character to Player or something else.

Underneath you find "Tag" change it to **"Player"** to let the game know this the character your moving or controlling. 

Then go on ground and add a "Box collider".

## 2. Create a Scripts called Player

Create a folder called Scripts right click and you see create hover over it and go to C# script then change the name to Player drag it onto your player character.

Double click on the script and wait for it to open.

We going to make the Player be able to Jump over the obstacles in this Script.

First we make a two private variable one called "CharacterController character and the other called Vector3 direction.

We will need a variable to allow us to modify the character's position.
We can use a reference to the player's character controller component for that. 


,,,
    
    private float CharacterController character
    
    private Vector3 direction; 

,,,

Now add two public float called gravity and give a value of 9.81f and times it by two and the other is jumpForce 8f. 
The gravity is is roughly close to real life gravity then adjust to how you want it the game.

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

Then go to void Update so we add join our variables together.

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

## 3. Game Speed

Create a new Script called GameManager then double click on it to open then in the **"Hierarchy"** create a empty game object call it Game Manager and drag the script on too it.

In the script create a public static GameManager called Instance and make the get public and set private

,,,

    public static  GameManager Instance { get; private set;}

,,,

Then we add three public float called gameSpeedIncrease with a value 0.1f, initialGameSpeed 5.0f and gameSpeed (make the get public and set private)

game speed Increase and game speed allows you to fasten your game speed as long you keep playing and the initial game speed is how fast you game originally runs.



So the code below us allows us to make a public variable so we can link it to other scripts later on.

,,,

    public float gameSpeedIncrease = 0.1f
    public float InitialGameSpeed = 5.0f
    
    public float gameSpeed {get; private set;}


,,,

Add a private void called Awake add a if statement saying this instance(Game Manager) saying if there more then one destroy it.

This code below us is saying that if the Instance is empty then spawn if not destroy.     
,,,


     private void Awake()
    {
        if(Instance == null) 
        {
            Instance = this;
        }
        else
        {
            DestroyImmediate(gameObject);
        }
     }

,,,

Make it a private void called Destroy add instance which can process the code above. 

The code below is apply to the code Destroy Immediate and making it happen. 

,,,

    private void OnDestroy()
    {
        if (Instance == this)
        {
            Instance = null;
        }
    }

,,,

Make another private void called New Game add in gameSpeed = InitialGameSpeed;

game speed = Initial game speed means that when the game speed changes so does the initial speed.

The reason why we need the new void(New Game) is because when the game ends you can start a new version immediately.



,,,

    private void NewGame() 
    {
        gameSpeed = initialGameSpeed;
    }

,,,

Go to void Start and add the new void you just made into it.

void Start is when you click play the action an happens once until you start again. So we when press play we get a fresh game to play. 


,,,

    private void Start()
    {
        NewGame();
    }

,,,

Go to void Update and add in gameSpeed, gameSpeedIncrease and Time deltaTime which basically over time the game will increase it's speed the longer you play.

,,,

    private void Update()
    {
        gameSpeed += gameSpeedIncrease * Time.deltaTime;
    }
,,,

## 4.Ground/Side-scrolling

First we create a new script called "**Ground**" drag the script into ground sprite. 

Go to the ground sprite and remove sprite renderer and add in ** Mesh Filter and Mesh Renderer**

Click on round circle on the right hand side of the **Mesh Filter** and select **Quad**

Create a new folder called **Materials** open it right click select create and go to **Materials** change the name to **Ground**. 

Go to **Shader** at the top of the Material change it to unlit **transparent** or **Texture** depend on your sprites.

Then drag the ground sprite into the texture box on the right and drag the ground material to the ground sprite.

Go back to ground sprite and change the scale value to what the sprite pixel after its divided.

Reset you collider either by delete it and add in another one or reset it by click on the three dot on you right and select reset.

Change the center y value and size z value back to what it was before the change.

Go to you **Ground** script add in a private mesh renderer called meshRenderer.

mesh renderer is basically allow you to have a 3D character instead of 2D sprite character.

The code below is saying make a private mesh renderer give it name.

,,,

     private MeshRenderer meshRenderer;
,,,

Make a private void called Awake add in mesh renderer get component(Telling the system to get the mesh renderer) 
,,,

    private void Awake()
    {
        meshRenderer = GetComponent<MeshRenderer>();
    }

,,,

Go to void Update add a float called **speed** connect to Instance(GameManager) and the game speed and location where you want the increase in speed.

Connect the mesh renderer to the material and the texture and add the float speed so that when you play the ground moving faster the longer you play the game.

Vector 2 is like Vector3 but only in two axis instead of three which are x and y axis.
,,,

    private void Update()
    {
        float speed = GameManager.Instance.gameSpeed / transform.localScale.x;
        meshRenderer.material.mainTextureOffset += Vector2.right * speed * Time.deltaTime;
    }
,,,

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

Add in frame ++ to animate to increase the frame rate. 

Then add in if statement saying check if the frame is greater or equal to sprites length then return to zero. 

Then Add in another if statement making sure that the frame will stay in bounds of the array.

 Once animate has be called inkoke the animate by 1 sec / game manager instance game speed.

 Add in invoke name of Animate 0 sec to call this function after the game manager void start.

 Add in private void called OnDisable to get rid of the animation when not in use.

 The code is simple saying that when animation enabled start up the animation when not in use stop animating. 

 This need to be able to allow the character to be have an animation and then stop animation when not in use.
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
        if ( frame >= 0 && frame < sprites.Length) 
        {
            spriteRenderer.sprite = sprites[frame];
        }

        Invoke(nameof(Animate), 1f / GameManager.Instance.gameSpeed); 
        }
,,,

 After you finish this add the script to the player and go to the sprites section in the animated sprites script and click on the plus sign and add in you running animations.

 ## 6. Prefabs

Create a Prefab Folder. In Heirarchy drag the the obstacles sprites add a  "Obstacle Tag".

The reason why we use tag is so the system knows what we refer to when added in code later.

Add a Box Collider and change the order layer to one to all of them. If you have an flying obstacle add the Animated Spite script to it. 
Click the plus sign and add how many movements you have of that obstacle.

A Box Collider allows us the player or object to collider with each other instead of going through each other.

if you made the space in you sprite too big you can adjust it using the Box Collider.

You can adjust the size of the box collider if it too big or too small.

## 7. Spawner


 













 
