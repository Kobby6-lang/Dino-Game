# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

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

A Mesh Filter component holds a reference to a mesh. It works with a Mesh Renderer component on the same GameObject the Mesh Renderer renders the mesh that the Mesh Filter references.

The code below is saying make a private mesh renderer call it meshRenderer.

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