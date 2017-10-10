```swift
//
//  DropCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/21/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Drop Command 
 Used for player to drop an item 
 */
class DropCommand: Command {
    
    override init() {
        super.init()
        self.name = "drop"
    }
    
    //Executes drop function on player
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        if hasSecondWord() {
            //player should provide the name of the item they want to drop
            //the name of the items are the same as their planet names (which is also the name of their location)
            //with the exception of home, whose object is key and it must be called key
            player.drop(secondWord!)
        } else {
            //player must type a second word with this command or they will get an error
            player.warningMessage("\nWhat are you trying to drop?")
        }
        return false
    }
}
```