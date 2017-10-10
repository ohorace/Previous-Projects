```swift
//
//  GoCommand.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Go Command allows player to change locations
 */
class GoCommand: Command {
    
    override init() {
        super.init()
        self.name = "go"
    }
    //Function executed on player object to move to different locations
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        if hasSecondWord() {
            player.walkTo(secondWord!)
        } else {
            player.warningMessage("\nGo Where?")
        }
        return false
    }
}
```
