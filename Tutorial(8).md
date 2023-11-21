# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 8. Obstacles

Create a Obstacle scripts.

This script will allow us make the prefabs look like it moving towards the player when it's really not.

In the private void called Update you add in tranform position += vector3 left times the the game speed of the game.

Meaning that the obstacles will  match the speed of the ground and speed of the game and look like its moving.

Time.deltaTime is the interval in seconds from the last frame to the current one.



,,,

    void Update()
    {
        transform.position += Vector3.left * GameManager.Instance.gameSpeed * Time.deltaTime;
    }

,,,

Create private float called left edge. 

This variable allows to store a variable to use to destroy the objects after it leaves the screen.
,,,

    private float leftEdge;

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

We need to verify the **"other"** that were colliding with is the obstacle. Shown in the code below.

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

When the object has been found it mens a new game has started.

the code in void game over means disable everything when the player loses the game.

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

In the New Game void renable the player which we will be shown below. 

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