```swift
//
//  RandomCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/22/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Ramdon Command takes the player to a random room
 */
class RandomCommand: Command {
    
    override init() {
        super.init()
        self.name = "random"
    }
    
    //Function executes the random command on the player
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //a second word should not be entered
        //the randomRoom function randomizes the next location based on the current room
        if hasSecondWord() {
            player.warningMessage("\nYou can't randomize that")
        } else {
            player.randomRoom()
        }
        return false
    }
}
```