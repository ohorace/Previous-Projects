```swift
//
//  GetCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/19/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Get Commands is used to pick up objects
 */
class GetCommand: Command {
    
    override init() {
        super.init()
        self.name = "get"
    }
    
    //Function executes on the player object to allow them to pick up an object
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //player needs to enter the name of the object they want to pick up
        //Each object's name is the same as the planet's name with the exception of Home, it's object is named key
        if hasSecondWord() {
            player.getObject(secondWord!)
        } else {
            player.warningMessage("\nWhat do you want to get?")
        }
        return false
    }
}
```