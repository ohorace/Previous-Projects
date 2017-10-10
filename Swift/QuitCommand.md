```swift
//
//  QuitCommand.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation
/*
 Quit Command ends the game
 */
class QuitCommand: Command {
    
    override init() {
        super.init()
        self.name = "quit"
    }
    
    //Function executes on the player
    //@param player, player object
    //@return bool, false if the player enters a second word
    //will return true if the player does not enter a second word
    override func execute(player: Player) -> Bool {
        var answer : Bool = true
        //quit should be entered by itself and the player will have quit playing
        if hasSecondWord() {
            player.warningMessage("\nI cannot quit \(secondWord)")
            answer = false
        }
        return answer
    }
}
```