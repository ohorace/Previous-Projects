```swift
//
//  BackCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/18/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Back Command is used to return to the last visited location
 */
class BackCommand: Command {
    
    override init() {
        super.init()
        self.name = "back"
    }
    
    //Function executes on the player to return them to the previous location
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //player should only enter the word back
        if hasSecondWord() {
            player.warningMessage("\n You can only return to your previous location!!")
        } else {
            //will execute the enterRoom command with the location of the returnToRoom command
            player.enterRoom(player.returnToRoom())
        }
        return false
    }
}
```