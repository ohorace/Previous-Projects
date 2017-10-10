```swift
//
//  ResetCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/23/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Restart command allows user to start the game over from the beginning
 */
class RestartCommand: Command {
    
    override init() {
        super.init()
        self.name = "restart"
    }
    
    //Function executes the restart command on the player
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        if hasSecondWord() {
            player.warningMessage("\nYou can't do that! Please return Home")
        } else {
            player.restart()
        }
        return false
    }
}
```