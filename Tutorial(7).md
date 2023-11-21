# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

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