# FiveM-Scripts
My Public FiveM Scripts

## mhacking
The hacking minigame is inspired by the Hacking Minigame of Alpha Protocol, notoriously known for being horrible to play. You need to find two constant hex code blocks in a fast enough changing table of hexcode. It is purely a visual minigame. In the screen below you will see the left block hovering directly above a solution -- need to move it one down and press space to be accepted as a correct solution.

### Sample Implementation
```
function mycb(success, timeremaining)
	if success then
		print('Success with '..timeremaining..'s remaining.')
		TriggerEvent('mhacking:hide')
	else
		print('Failure')
		TriggerEvent('mhacking:hide')
	end
end


Citizen.CreateThread(function()
  while true do
    Citizen.Wait(0)
    if IsControlJustReleased(1,213) then -- Home key
	  TriggerEvent("mhacking:show")
	  TriggerEvent("mhacking:start",7,35,mycb)
    end
  end
end)
```

### Changelog

#### 20171225
* Initial Release
#### 20180102
* Fixed mhacking not reseting mistakes
#### 20180110
* Added time remaining in ms as a second parameter for the callback function;
* If the player dies, the script now sets the remaining time to 0, and fails the player. 
* Added `mhacking:setmessage` to set messages while waiting for feedback 
* Added `sequentialhack.lua` to handle sequentialhacks without everyone needing to program their own implementation, which can be removed from the `__resource.lua` if one does not need it.
