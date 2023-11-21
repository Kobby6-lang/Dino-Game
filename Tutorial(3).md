# Dino Game Tutorial

I used this code from https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 3. Game Speed

Create a new Script called **GameManager**, then double click on it to open, then, in the **"Hierarchy"**, create an empty game object, call it Game Manager and drag the script onto it.

In the script, create a public static GameManager called Instance and make the get public and set private.

,,,

    public static  GameManager Instance { get; private set;}

,,,

Then we add three public floats called gameSpeedIncrease with a value 0.1f, initialGameSpeed 5.0f and game speed (make the get public and set private)

Game speed Increase, and game speed allows you to fasten your game speed as long you keep playing, and the initial game speed is how fast your game originally runs.



So, the code below allows us to make a public variable to link it to other scripts later.

,,,

    public float gameSpeedIncrease = 0.1f
    public float InitialGameSpeed = 5.0f
    
    public float gameSpeed {get; private set;}


,,,

Add a private void called Awake add a if statement saying this Instance (Game Manager) saying if there more then one destroy it.

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

Make a private void called Destroy and add the Instance to process the code above. 

The code below applies to Destroy Immediate and makes it happen. 

,,,

    private void OnDestroy()
    {
        if (Instance == this)
        {
            Instance = null;
        }
    }

,,,

Make another private void called New Game. Add in-game speed = InitialGameSpeed;

Game speed = Initial game speed means that when the game speed changes, so does the initial speed.

We need the new void(New Game) because you can start a new version immediately when the game ends.



,,,

    private void NewGame() 
    {
        gameSpeed = initialGameSpeed;
    }

,,,

Go to void Start and add the new void you just made.

Void Start is when you click to play the action, which happens once until you start again. So when we press play again, we get a fresh game. 


,,,

    private void Start()
    {
        NewGame();
    }

,,,

Go to void Update and add in gameSpeed, gameSpeedIncrease and Time deltaTime, which, over time, the game will increase its speed the longer you play.

,,,

    private void Update()
    {
        gameSpeed += gameSpeedIncrease * Time.deltaTime;
    }
,,,
