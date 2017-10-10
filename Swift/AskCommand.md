```swift
//
//  AskCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/20/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Ask Commands allows a player to find out what is in a location
 */
class AskCommand: Command {
    
    override init() {
        super.init()
        self.name = "ask"
    }
    
    //Function executes the command to ask for the items in a location
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //player must type the name of the location they want to ask along with the command word
        if hasSecondWord() {
            player.askForItem(secondWord!)
        } else {
            player.warningMessage("\nYou must ask this location!")
        }
        return false
    }
}
```