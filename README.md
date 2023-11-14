# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s
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
        if ( frame <= 0 && frame < sprites.Length) 
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

Create a Spawner Script the Spawner allows us to spawn the objects or obstacles we want in our game.

Whether it's slow or fast spawns that we want.

In the Script add in a public struct variable called spawnableObject.

Which allows us to spawn multiple prefabs sprites at different intervals.

In the struct variable add in the a public gameObject named prefab.

the **struct** variable allows to find the prefabs and spawn them in our game.

,,,

    public struct SpawnableObject 
    {
       public GameObject prefab;
    }

,,,

Add in a public float called spawnChance which allows the system to randomise the spawn time of the prefabs.

Add in the range of 0 to 1 shown below this tells the system the spawnChance is between 0 and 1.

    public struct SpawnableObject 
    {
       public GameObject prefab;
       [Range(0f, 1f)]
       public float SpawnChance;
    }
,,,

Now we going to create an array of spawnable objects allow us to apply the code above to our game.

This won't show up on the editor because it doesn't know how to serialise it so the editor can understand it.

So go to the top and add in system serializable which allow the system to convert it to something that understandable.

    [System.Serializable]

    public SpawnableObject[] objects;

Then go to **"Hierarchy"** add in empty gameObject reset the position back to zero and add in you script.

Then you will see objects on scripts click the plus seven times or add the number 7 to the box on the right hand side.

There will add in the prefabs from spawn more to spawn less in your game.

Don't forget to add in numbers in the spawnChance below the prefab a number between 0 and 1 of your choice.

Make two public floats called minSpawnRate and maxSpawnRate.

It basically allows to spawn our objects between 1 and 2 secs.

    public float minSpawnRate = 1f;
    public float maxSpawnRate = 2f;

Add in a private void called OnEnable allows the system to enable the randomisation of the spawn rates intervals.

    private void OnEnable() 
    {
        Invoke(nameof(Spawn), Random.Range(minSpawnRate, maxSpawnRate));
    }
,,,

Make another private void called Spawn allowing us to call the code above otherwise we get an error.

Add in private void called OnDisable allowing us to disable the code when not needed.

    private void OnDisable()
    {
      CancelInvoke();
    }
,,,

Add in the spawnChance float that allows to pick a random number between 0 and 1.

To go through our loops(array) if objects(obj for short) is less than our spawn chance then go ahead and spawn the object.

So if the object has been spawn then whenever it is go to the other direction heading to the player position.

Then you add break shown below allows to not continously spawn objects.

If the object does not meet the requirement to spawn then go to the next number on the array until requirement has been met. 

If the object has been called then we call our invoke again and pick another number between min and mix to spawn another object.

    private void Spawn()
    {
       float spawnChance = Random.value;

        foreach (var obj in objects) 
        {
            if(spawnChance > obj.spawnChance) 
            {
                GameObject obstacle = Instantiate(obj.prefab);
                obstacle.transform.position += transform.position;
                break;
            }

            spawnChance -= obj.spawnChance;
        }

        Invoke(nameof(Spawn), Random.Range(minSpawnRate, maxSpawnRate));
     }

,,,

## 8. Obstacles

Create a Obstacle scripts.

This script will allow us make the prefabs look like it moving towards the player when it's really not.

In the private void called Update you add in tranform position += vector3 left times the the game speed of the game.

you also add **Time.deltaTime** meaning that you can control the speed you want time to go.

Meaning that the obstacles will move to match the speed of the ground and speed of the game.

,,,

    void Update()
    {
        transform.position += Vector3.left * GameManager.Instance.gameSpeed * Time.deltaTime;
    }

,,,

Create private void called left edge. 

This variable allows to store a variable to use to destroy the objects after it leaves the screen.
,,,

    private void leftEdge;

,,,

,,,

The code allows us to connect the float. 

We just created with the main camera saying that when the objects exits out of the view of camera(x) destroy it after 2 secs. 

    private void Start()
    {
        leftEdge = Camera.main.ScreenToWorldPoint(Vector3.zero).x - 2f;
    }
,,,


The if statement is saying once (x) is less than left edge then destroy it if not wait until then.
,,,

    void Update()
    {
        transform.position += Vector3.left * GameManager.Instance.gameSpeed * Time.deltaTime;

        if (transform.position.x < leftEdge)
        {
            Destroy(gameObject);
        }
    }

Then add the script to all of your prefabs when done with the code section.
,,,

Click on the Player Scripts.

Add in private void called OnTriggerEnter.

On TriggerEnter allows you to say when hit or crash into something then trigger an appropiate reponse to the situation.

We need to verify the **"other"** that were colliding with is tthee obstacle. Shown in the code below.

This need to be matched with the obstacle tag we made earlier otherwise it won't work.
,,,

    private void OnTriggerEnter(Collider other)
    {
        if(other.CompareTag("Obstacle"))
        {
           
        }
    }

,,,

We create a public void called GameOver. Where we disable the game speed and everything else as well. Shown below.
,,,

    public void GameOver()
    {
        gameSpeed = 0f;
        enabled = false;
    }

,,,

We need to deactive our player and spawner so let create a variable for this two.
,,,
    private Player player;
    private Spawner spawner;

,,,

The code is saying find the object of this variable and do something with it when the code has been written. 

,,,
        {
          player = FindObjectOfType<Player>();
          spawner = FindObjectOfType<Spawner>();


          NewGame();
       }
,,,

,,,

    public void GameOver()
    {
        gameSpeed = 0f;
        enabled = false;
        player.gameObject.SetActive(false);
        spawner.gameObject.SetActive(false);
    }
,,,

In the New Game void reenable the player which we will be shown below. 

We also need to clean up all the obstacles in the array. We find this using the find objects code.

Then we add a for each statement saying every objects we find in our array destroy every time we start a new game.

    private void NewGame() 
    {
        Obstacles[] obstacles = FindObjectsOfType<Obstacles>();

        foreach(var obstacle in obstacles) 
        {
            Destroy(obstacle.gameObject);
        }

        gameSpeed = initialGameSpeed;
        enabled = true;
        player.gameObject.SetActive(true);
        spawner.gameObject.SetActive(true);
    }

## 9. UI

Create a Font folder where you will add in a font you created yourself or took from the internet. 

Then you convert it to a textmeshpro mesh.

We can do this by right clicking and going to create and look for textmesh pro and click on font assest.

Or we go to windows textmesh pro and go to font assest creator and add in your font and click save.

Before we add in the text we right click on heirarchy and go to canvas.

Canvas allows as to project something onto the screen.

If it's you first time creating a textmeshpro then you get a popup saying import tmp essentials click on and wait for a bit and close it down afterwards.

Then right click on canvas to add a child to it named game over or something else and click on textmeshpro text add in your font on the right hand side where it says font asset.

Go to the canvas right click again and click on button textmeshpro.

Drag your gameover button to the source image on buttom tmp and set to native size and delete the text child underneath.

You then adjust you font and button to your preferences on the right hand side.

Go to button scroll down until you see On click and click the + button.

Add in GameManager game object on the heirarchy if you add in the script game object it won't work. 

Then click on no functions and go to GameManager and find **new game** you might not find it because it set to private so go back to the code change it to public.

So go to the game manager script and change it.

Once done go to no function and click on game manager and you will see new game click on that and go back to game manager script.

Then go to the very top of the script and add in using TMPro and using unityEngine UI.

This two code allows the system to know that you're using these variable in your game.
,,,

    using TMPro;
    using UnityEngine.UI;

,,,

Add a public variable TextMeshproUGUI called gameOverText and a public variable button called RetryButton.

These Variables allows to reference the text and button in our scene when we drag our game objects  on to them later.

    public TextMeshProUGUI gameOverText;
    public Button retryButton;

,,,

Go to the new game void add in game over text game object set active false and the same for  retry button.

This code are saying that if you are in a new disable the ui canvas.

    gameOverText.gameObject.SetActive(false);
    retryButton.gameObject.SetActive(false);

,,,

Go to game over void and copy in the code at the top and change both to true.

,,,

    gameOverText.gameObject.SetActive(true);
    retryButton.gameObject.SetActive(true);

,,,

This is saying once you fail or die the system will renable the UI canvas.

Go back to the heirarchy assign the text and button in the game manager otherwise you will get an error saying that can't find reference or something like that.

























 













 
