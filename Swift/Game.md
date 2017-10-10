```swift
//
//  Game.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/17/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

class Game {
    var player : Player?
    var parser : Parser
    var playing : Bool
    
    //Initializer to create Game
    init(gameIO : GameOutput) {
        playing = false
        parser = Parser(newCommands: CommandWords())
        player = Player(room: GameWorld.sharedInstance.entrance!, output: gameIO)
    }
    
    //Function signals the start of the game
    //Prints the welcome message
    func start() {
        playing = true
        player?.outputMessage(welcome())
    }
    
    //Function signals the end of the game
    //Prints the goodbye message
    func end() {
        playing = false
        player?.outputMessage(goodbye())
    }
    
    //Function prints a welcome message with minimal instructions
    //Function displayes the current room
    func welcome() -> String {
        let message = "This is Princess Serenity, Princess of the Moon!\nI need your help, please find the 4 Inner Sailor Scouts and bring me their brooches.\nGeneral information: Drop: drop item\nRestart: start over\nGo: travel in a direction\nBack: go back to previous location\nAsk: find out what's available\nRandom: go to random location\nQuit: stop playing\nGet: pick up an item\nLock: lock or unlock room\nView: view objects you have\n\nType 'help' if you need help."
        return "\(message)\n\n\(player!.currentRoom.description())"
        
    }
    
    //Function prints a goodbye prompt after they quit
    func goodbye() -> String {
        return "\nThank you for playing, Goodbye.\n"
    }
    
    //Function executes the command typed from the keyboard
    func execute(commandString : String) -> Bool {
        var finished : Bool = false
        if playing {
            player?.commandMessage("\n\(commandString)")
            let command : Command? = parser.parseCommand(commandString)
            if command != nil {
                finished = (command?.execute(player!))!
            } else {
                player?.errorMessage("\nI don't understand...")
            }
        }
        return finished
    }
}
```