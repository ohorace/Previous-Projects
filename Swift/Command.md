```swift
//
//  Command.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Super Class Command
 Sets name of command
 */
class Command {
    var name : String
    var secondWord : String?
    
    init() {
        self.name = ""
    }
    
    //Function to see if there is a second word
    //@preturn bool, returns false if second word is nil and true if it is not
    func hasSecondWord() -> Bool {
        return secondWord != nil
    }
    
    //Function to execute command on player
    //@return bool, returns false
    //This function is overridden in subclasses
    func execute(player : Player) -> Bool {
        return false
    }
}
```
