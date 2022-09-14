# UnityLocalMultiplayer
A small guide to a local multiplayer game in unity

### Setting up the action map

If you want to make a local multiplayer game the easiest way is to use the new input system.

Start of by making a new action map and adding your controlls. (we will use this for both players. Don't mind the P1)

// IMAGE 

After making all the controlls, make a controll scheme for each controller (I will use WASD and Arrows on the same keyboard).

// image

### Player scripts

Now add the PlayerInput script to your players and set the Actions to the action map you just made.
Then change the behavior to "Invoke Unity Events".

/7 image

After that is done we will create the player script. I will simply use a rigidbody2D for the simplicity.

This script will be very simple in this guide but also quite scalable

```csharp
using UnityEngine;
using UnityEngine.InputSystem;

[SerializeField] private float mSpeed;
Rigidbody2D rb;
Vector2 moveDir;

private void Start() => rb = GetComponent<Rigidbody2D>();

// This is the function we will be controlling in the PlayerInput script
public void OnPlayerMove(InputAction.CallbackContext ctx) => moveDir = ctx.ReadValue<Vector2>();

private void Update()
{
  rb.AddForce(moveDir * mSpeed, ForceMode2D.Force);
}
```
After making this script we can simply add it to the player.

In the PlayerInput script we can now open up the "Events" tab and then the "player" tab (the name of your player object)

// Image

Now you can simply press the + and add your player move script like with a simple UI button.

Now for spawning the players we can simply make a new small script and place it on an empty object.

This script will simply spawn both players with the right controll scheme on the same keyboard. 
This is only done because by default Unity won't allow you to spawn 2 players using the same keyboard with the PlayerInputManager script.

This script is also quite simple

```csharp
[SerializeField] private GameObject playerPrefab;

private void Start()
{
// Keyboard and Arrows will have to be changed to your controll scheme names
  var player1 = PlayerInput.Instantiate(playerPrefab, controlScheme: "Keyboard", pairWithDevice: Keyboard.current);
  var player2 = PlayerInput.Instantiate(playerPrefab, controlScheme: "Arrows", pairWithDevice: Keyboard.current);
}
```

And this will spawn two players using the same keyboard but different control schemes
