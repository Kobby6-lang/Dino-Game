# Dino Game Tutorial

I used this code from: https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 9. UI

Create a Font folder where you will add in a font you created yourself or took from the internet. 

Then you convert it to a textmeshpro mesh.

We can do this by right clicking and going to create and look for textmesh pro and click on font assest.

Or we go to windows textmesh pro and go to font assest creator and add in your font and click save.

Before we add in the text we right click on heirarchy and go to canvas.

Canvas allows as to project something onto the screen.

If it's you first time creating a textmeshpro then you get a popup saying import tmp essentials click on and wait for a bit and close it down afterwards.

Then right click on canvas to add a child to it name it game over or something else and click on textmeshpro text add in your font on the right hand side where it says font asset.

Go to the canvas right click again and click on button textmeshpro.

Drag your gameover button sprit to the source image on buttom tmp and set to native size and delete the text child underneath.

You then adjust you font and button to your preferences on the right hand side.

Go to button scroll down until you see On click and click the + button.

Add in GameManager game object on the heirarchy if you add in the game manager script it won't work. 

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

Go to the new game void add in game over text game object set active false and the same for retry button.

This code are saying that if you are in a new game disable the ui canvas.

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