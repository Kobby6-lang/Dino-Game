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


,,,
    
    private float CharacterController character
    
    private Vector3 direction; 

,,,

Now add two public float called gravity and give a value of 9.81f and times it by two and the other is jumpForce 8f. 
The gravity is is roughly close to real life gravity then adjust to how you want it the game.
,,,

    { public float gravity = 9.81f * 2f;
      public float jumpForce = 8f;
    }
    

,,,

We going to add a private void called Awake. Which we add character get component CharacterController
,,,

    private void Awake()

    {
      character = GetComponent<CharacterController>();
    }

,,,

After this we add another private void called OnEnable then we add direction variable.

,,,
   
    private void OnEnable() 
    {
      direction = Vector3.zero;
    }

,,,

Then go to void Update so we add join our variables together. 
This code is basically saying if you press the space button to jump the gravity pressure will stop you from jumping too high.

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

,,,

    public float gameSpeedIncrease = 0.1f
    public float InitialGameSpeed = 5.0f
    
    public float gameSpeed {get; private set;}


,,,

Add a private void called Awake add a if statement saying this instance(Game Manager) saying if there more then one destroy it.
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

,,,

    private void NewGame() 
    {
        gameSpeed = initialGameSpeed;
    }

,,,

Go to void Start and add the new void you just made into it.

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

Go to you **Ground** script add in a private mesh renderer called Meshrenderer.

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
,,,

    public Sprite[] sprites;
    private spriteRenderer spriteRenderer

,,,

Add in a private void Awake and inside the brackets add in sprite Renderer get the components of the spriteRenderer variable.

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

 Once animate has be called inkoke the animate by 1 sec / game manager instance. game speed.

 Add in invoke name of Animate 0 sec to call this function after the game manager void start.

 Add in private void called OnDisable to get rid of the animation when not in use.
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

 After you finish this add the script to the player and go to the sprites section and click on the plus sign and add in you running animations.

 ## 6. Prefabs
 













 
