# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

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

Make a private void called Destroy add instance which can process the code above. 

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

void Start is when you click play the action an happens once until you start again. So we when press play again we get a fresh game to play. 


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