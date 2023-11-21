# Dino Game Tutorial

I used this code from https://github.com/zigurous/unity-dino-game-tutorial /
https://www.youtube.com/watch?v=UPvW8kYqxZk&t=5304s

## 9. UI

Create a Font folder where you will add a font you created yourself or took from the internet. 

Then, you convert it to a text mesh pro mesh.

We can do this by right-clicking and going to **create** and look for Text Mesh Pro, and click on font asset.

Or we go to Windows text mesh pro, Font Assest Creator, add your font, and click save.

Before we add in the text, we right-click on hierarchy and go to the canvas.

Canvas allows us to project something onto the screen.

If it's your first time creating a text mesh pro, you get a popup saying import tmp essentials. Click on wait for a bit and close it down afterwards.

Then right-click on canvas to add a child, name it Game Over or something else and click on text mesh pro text add in your font on the right-hand side where it says font asset.

Go to the canvas, right-click again, and click on the button text mesh pro.

Drag your game over button sprite to the source image on button tmp set to native size and delete the text child underneath.

You then adjust your font and button to your preferences on the right-hand side.

Go to the button, scroll down until you see **on click** and click the + button.

Add in the GameManager game object on the hierarchy. If you add in the game manager script, it won't work. 

Then click on no functions, go to GameManager, and find **new game**. You might not find it because it is set to private, so go back to the code and change it to public.

So go to the game manager script and change it.

Once done, go to no function, click on Game Manager, and you will see **new game**. Click on that and go back to the game manager script.

Then go to the very top of the script and add in using TMPro and using unityEngine UI.

These two codes let the system know you're using these variables in your game.
,,,

    using TMPro;
    using UnityEngine.UI;

,,,

Add a public variable TextMeshproUGUI called gameOverText and a public variable button called RetryButton.

These Variables allow us to reference the text and button in our scene when we drag our game objects onto them later.

    public TextMeshProUGUI gameOverText;
    public Button retryButton;

,,,

Go to the new game void and add in the **game over** text game object set active false and the same for **retry button**.

This code says to disable the UI canvas if you are in a new game.

    gameOverText.gameObject.SetActive(false);
    retryButton.gameObject.SetActive(false);

,,,

Go to game over void copy in the code at the top and change both to true.

,,,

    gameOverText.gameObject.SetActive(true);
    retryButton.gameObject.SetActive(true);

,,,

This is saying once you fail or die, the system will enable the UI canvas.

Go back to the hierarchy and assign the text and button in the game manager; otherwise, you will get an error saying that can't find a reference or something like that.
