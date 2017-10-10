```swift
//
//  Parser.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

class Parser {
    //variable of commands of type CommandWords
    var commands : CommandWords
    
    //initializer to set commands
    init(newCommands : CommandWords) {
        commands = newCommands
    }
    
    //Function to parse command and separate it into words
    //@param commandString, line tyoed by the user to be executed
    //@return comamand, returns the first word of the string which is the actual command word
    func parseCommand(commandString : String) -> Command? {
        
        var command : Command? = commands.get("")
        let words = commandString.componentsSeparatedByString(" ")
        if words.count > 0 {
            command = commands.get(words[0])
            if command != nil {
                if words.count > 1 {
                    command?.secondWord = words[1]
                } else {
                    command?.secondWord = nil
                }
            }
        }
        
        return command
    }
    
    //Function prints a description of the command
    //@return String, command description
    func description() -> String {
        return commands.description()
    }
}
```
