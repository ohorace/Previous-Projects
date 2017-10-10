```swift
//
//  LockCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/21/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation
/*
 Lock Command locks AND unlocks
 */
class LockCommand: Command {
    
    override init() {
        super.init()
        self.name = "lock"
    }
    
    //Function executes on the player to allow the player to lock or unlock a room
    //@precondition the room that the player is attempting to (un)lock must be the Moon Kingdom
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //player must enter the name of the room they wish to lock
        //instead of entering 'lock Moon Kingdom' (which would require three words) the player only needs to enter 'lock moon'
        if hasSecondWord() {
            player.lockOrUnlock(secondWord!)
        } else {
            player.warningMessage("\nWhat are you trying to lock or unlock? (one word only)")
        }
        return false
    }
}
```
