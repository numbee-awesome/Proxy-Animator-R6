### What does this do: 

Adds paired leg animation functionality without having to change the core R6 rig by manipulating .Transform property of Motor6D instances

Reads through a table of animations and uses CFrame math to inverse offset the R6 torso's animation for R6 legs to animate independently of the Torso's .Transform

.rbxl example place is linked along with .rbxm with the modulescript, drag and drop .rbxm for install (more detailed install and module code here soon)

# Examples

<img width="816" height="490" alt="RobloxStudioBeta_dI3gH1RpxP" src="https://github.com/user-attachments/assets/be0ca5aa-1e4b-4491-8ca4-d3953a898961" />
<img width="378" height="439" alt="RobloxStudioBeta_M5IY3d3dfj-ezgif com-optimize" src="https://github.com/user-attachments/assets/b6bef5b7-f321-4c67-a21f-9fd30aaed247" />

*notice how the legs are moving independently from the r6 torso (again this does NOT modify the R6 rig)


# Methods

## ProxyAnimate.new(CHR: Model, ProxyAnimList: {}, isParallel: boolean)

  creates new ProxyAnimate class that tracks CHR (Player's Character) with a needed passed player Character and table list of animations needed to animate independently from the torso, there is an optional isParallel bool for parallel support

  tracks character's playing animations and detects whether tracked animation is under the ProxyAnimList table and does the leg offset stuff

```lua
local ProxyAnimate = require(ReplicatedStorage:WaitForChild("ProxyAnimateClass"))
local PROXY_ANIMATIONS_LIST = {} --insert list of animations here eg) { [AnimationID] = Animation }

local PLR = game.Players.LocalPlayer	
local CHR = PLR.Character or PLR.CharacterAdded:Wait()

local chrProxy = ProxyAnimate.new(CHR, PROXY_ANIMATIONS_LIST)

```

## ProxyAnimate:SteppedUpdate(optionalParallel: boolean)

  hook this onto a .Stepped OR .PreSimulation loop and the class will periodically update the .Transform of the player's character

  optionalParallel is available if you did not initially set it during class's initialization
  
```lua
RunService.PreSimulation:Connect(function(dt) --you can connect this in parallel under an actor (which is useful for NPCs)
	chrProxy:SteppedUpdate()
end)
```
