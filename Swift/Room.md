```swift
//
//  Room.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/16/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

//Room class contains the guidelines for creating a Room
//The room class also has a dictionary of objects to store items in Rooms
class Room {
    var exits : [String : Room]
    var tag : String
    var objects : [String : ScoutObjects]
    
    //Initializers set properties of Rooms
    convenience init() {
        self.init(tag: "No Tag")
    }
    
    init(tag : String) {
        exits = [String : Room]()
        self.tag = tag
        objects  = [String: ScoutObjects]()
    }
    
    //Function sets exits
    func setExit(exitName : String, room : Room) {
        exits[exitName] = room
    }
    
    //Function returns exits
    func getExit(exitName : String) -> Room? {
        return exits[exitName]
    }
    
    //Puts an object in the room
    //@param object, ScoutObject to add to room
    func drop(object : ScoutObjects){
        objects[object.getName()] = object
    }
    
    //Pick up an object from the room
    //@param objName, name of the object to be picked up
    //@return ScoutObjects, object that corresponds to the objName, this may be nil
    func pickUp(objName : String) -> ScoutObjects?{
        let object = objects[objName]
        if object != nil {
            objects.removeValueForKey(objName)
        }
        return object
    }
    
    //Checks if an object is still in the room
    //Used along with ask command to find out what object (if any) is in a room
    //@param name, name of object
    //@return bool, true if object is still in the room and false if the object is not in the room
    func hasObject(name : String) -> Bool{
        for nameKey in objects.keys {
            if objects[nameKey]?.getName() == name{
                return true
            }
        }
        return false
    }
    
    //Checks to see if the room has the key specifically
    //Works the exact same as the hasObject function
    func hasKey(name : String) -> Bool {
        for nameKey in objects.keys {
            if objects[nameKey]?.getName() == name{
                return true
            }
        }
        return false
    }
    
    //Returns objects in Room
    func printObjects() -> String{
        let objectList : [String] = [String](objects.keys)
        return "The following object(s) are located in this room: " + objectList.joinWithSeparator(" ")

    }
    
    //Gets exits from a particular room and returns a string of them
    func getExits() -> String {
        let exitNames : [String] = [String](exits.keys)
        return "Exits: " + exitNames.joinWithSeparator(" ")
    }
    
    //Returns a string containing the exits from a particular room
    func description() -> String {
        return "You are at \(tag).\n *** \(self.getExits())"
    }
    
    //Returns the tag of a room
    func getTag() -> String {
        return "\(tag)"
    }
    
    //Deinitializes room object
    deinit {
        tag = ""
        exits.removeAll()
    }
}
```
