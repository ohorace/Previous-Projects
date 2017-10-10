```swift
//
//  ViewCommand.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/27/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation
/*
 View commands allows the player to see what they have in their bag
 */
class ViewCommand: Command {
    
    override init() {
        super.init()
        self.name = "view"
    }
    
    //Function executes on the player to allow them to view what's in their bag
    //@param player, player object
    //@return bool, returns false
    override func execute(player: Player) -> Bool {
        //player only needs to enter 'view' no second word is needed
        if hasSecondWord() {
            player.warningMessage("\n'View' will be sufficient")
        } else {
            player.viewBag()
        }
        return false
    }
}
```