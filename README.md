# Next Level Roblox Development

> Pre-written scripts to assist sensei's and ninjas with coding along to the lesson plan.

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

> This script is attached to the chosen button like object and must match the given name, eg. "Button"

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
> NOTE: #tiles and #obstacles = local variables of the same name from previous Bug Fixing project

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
> Step 2: Add an effect part like fire that is disabled.
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
