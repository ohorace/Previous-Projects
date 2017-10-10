```swift
//
//  HelpCommand.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 The Help Command will should the player the list of commands they are able to use
 */
class HelpCommand: Command {
    //words will be the commandwords
    var words : CommandWords
    
    init(commands : CommandWords) {
        words = commands
        super.init()
        self.name = "help"
    }
    
    //Function executes the help command on the player
    //@param player, player object
    //@return bool, false
    override func execute(player: Player) -> Bool {
        //player should just enter the word help and the command will execute and print the list of commands available to the player
        if hasSecondWord() {
            player.warningMessage("\nI cannot help you with '\(secondWord!)'")
        } else {
            //words.description will print the command words
            player.outputMessage("\nAre you having trouble? Hurry the Princess needs you!\n\nYour available commands are:\n\(words.description())")
        }
        return false
    }
}
```
