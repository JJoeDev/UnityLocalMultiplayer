# UnityLocalMultiplayer
A small guide to a local multiplayer game in unity

### Setting up the action map

If you want to make a local multiplayer game the easiest way is to use the new input system.

Start of by making a new action map and adding your controlls.

// IMAGE 

After making all the controlls, make a controll scheme for each controller (I will use WASD and Arrows on the same keyboard).

// image

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

public void OnPlayerMove(InputAction.CallbackContext ctx) => moveDir = ctx.ReadValue<Vector2>();

private void Update()
{
  rb.AddForce(moveDir * mSpeed, ForceMode2D.Force);
}

```
