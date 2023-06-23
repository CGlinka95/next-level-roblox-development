# Next Level Roblox Development

> Pre-written scripts to assist senseis and ninjas with coding along the lesson plan.

## Day 1 - Color Changing Script:

```lua
local part = script.Parent
part.BrickColor = BrickColor.new("Dark blue")
```

> Parent: Any part
> 
> Trigger: When the game is loaded 
> 
> Result: The color of the brick changes to the one specified 
> 
> Customization: Change the name of the color on line 2

---

## Day 2 - Creating an instance:

### Adding A Part With Code

```lua
local domino = Instance.new("Part")
domino.Name = "domino"
--Add code for BrickColor here--
domino.Parent = game.Workspace
```

> Parent: Workspace
> 
> Trigger: When the game is loaded 
> 
> Result: A part named "domino" will spawn underneath the player when the game is loaded. Note: If your character is standing on top of a spawn location, the part will be hidden inside the spawn location block.
> 
> Customization: No customization for this yet.

### Creating A Function

```lua
function generateDomino()
  --Add code from the previous code block here--
end

--Call the function by its name below to execute the function--
generateDomino()
```

### Loops: Repeating an Action

```lua
for i = 2, 10, 2 do
  --Call the function by its name below to execute the function inside the for loop--
  generateDomino()
  wait(.5)
end
```

### Orientation

```lua
--Add this line of code inside the generateDomino() function--
domino.Orientation = Vector3.new(0, 0, 90)
```

> Note: Orientation refers to the rotation of a part. Any property with 3 values, needs Vector3.new() to be set in the code. The 3 values reference the x, y, and z coordinates on a plane.

### Using Parameters to Increment the Position of the Domino

```lua
function generateDomino(position)
  local domino = Instance.new("Part")
  --Apply the parameter to the Position property of the domino below--
  domino.Position = position
  domino.Orientation = Vector3.new(0, 0, 90)
  domino.Name = "domino"
  domino.BrickColor = BrickColor.Random()
  domino.Parent = game.Workspace
end

for i = 0, 20, 1 do
  --Pass the value of the parameter into the function below--
  generateDomino(Vector3.new(i, 0, 0))
  wait(.5)
end
```

> Result: A number of dominoes will spawn one by one until the for loop finishes. Add some space between the dominoes and KNOCK THEM DOWN!

---

## Day 3 - Hidden Path Challenge Script:

```lua
-- Touch event = .Touched
script.Parent.Button.Touched:Connect(function(hit)
  if not pathGenerated then
    pathGenerated = true
    print("Button pressed!")
    -- Below for loop that ninjas must copy & paste into their code to connect the path generation to the Touch event
    for i = 2, 60, 4 do
      generateDomino(Vector3.new(i, 0, 0))
      wait(0.3)
    end
  end
end)
```

> This script is attached to the chosen button-like object and must match the given name, eg. "Button"

---

## Finished Code for Invisible Tiles:

```lua
local timerChange = .1

-- Create boolean variable | NOTE: This can be called whatever you want!
local hackerMan = false
script.Parent.SecretObject.Touched:Connect(function(hit)
  print('Secret object acquired!')
  hackerMan = true
end)

-- Create function that hides the tiles:
function hideTiles(color)
  for i = 1, #tiles do
    if (tiles[i].BrickColor ~= color) then
      if hackerMan then
        tiles[i].Transparency = 0.4
        tiles[i].CanCollide = true
      else
        tiles[i].Transparency = 1
        tiles[i].CanCollide = false
      end
    end
  end
  for i = 1, #obstacles do
```

> IMPORTANT: bool name can be different and transparency can vary!
>
> NOTE: #tiles and #obstacles = local variables of the same name from the previous Bug Fixing project

---

## Additional Scripts:

### Trap Script (damages players when touched):

```lua
script.Parent.Touched:Connect(function(hit)
  if hit and hit.Parent and hit.Parent:FindFirstChild("Humanoid") then
    script.Parent.Fire.Enabled = true
    hit.Parent.Humanoid.Health -= 5
  end
end)
```

> Step 1: Add an object that you want to damage the player.
> Step 2: Add an effect part like a fire that is disabled.
> Step 3: Add a script and copy the above code. Make sure to use the name of the effect in the script!

> NOTE: Change the value on line 4 to do more or less damage

---

### Secret Door Script:

```lua
local function secretSwitchPressed(part)
  local parent = part.Parent
  if game.Players:GetPlayerFromCharacter(parent) then
    -- Not a typo since there is an object on top of an object!
    script.Parent.Parent.Parent.door:Destroy()
  end
end

script.Parent.Touched:Connect(secretSwitchPressed)
```

> Step 1: Add an object to use as a door or barrier.
> Step 2: Add an object to use as a hidden switch.
> Step 3: Add a script to the switch and copy the above code. Make sure to use the name of the door in the script!

> IMPORTANT: The script may not work if attached to certain models. Be sure to attach the script to a PART!
