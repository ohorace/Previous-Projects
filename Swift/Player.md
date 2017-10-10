```swift
//
//  Player.swift
//  StarterGame
//
//  Created by Rodrigo Obando on 3/16/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation
import Cocoa

class Player {
    var currentRoom : Room
    var io : GameOutput
    
    //keeps track of the last visited room by storing the value of the current room before it changes
    var previousRoom : Room
    //array to hold rooms to be able to use the 'Back' command
    var locationTracker : [Room] = []
    //back of objects will be used to store objects that the player gets
    var bag : [String : ScoutObjects]
    
    //generic room control object that is used to control (un)locking the Moon Kingdom
    var rc : RoomControl = RoomControl()
    
    
    init(room : Room, output : GameOutput) {
        currentRoom = room
        io = output
        previousRoom = currentRoom
        bag = [String : ScoutObjects]()
    }
    
    /*
     WalkTo() function takes a direction and progresses the player to the room located in that direction from the current room. Also, the room cannot be nil or the player will get an error message stating that there is no door in that direction.
     This function checks to see if the room in that direction is the Moon Kingdom. If it is, the player cannot enter unless the room is unlocked. Once the player is able to enter the room, this function also checks if the player has won by checking if their bag contains all the inner Sailor Scout objects.
     @param: direction, of type String
     */
    func walkTo(direction : String) {
        //add current room to locationTracker array before changing it, this is now the last visited room
        locationTracker.append(currentRoom)
        let nextRoom : Room? = currentRoom.getExit(direction)
        //if the location of the next room is not nil
        if nextRoom != nil {
            //first check if the next room is the Moon Kingom
            if(nextRoom?.getTag() == "Moon Kingdom") {
                //If the Room Control (which is only used for the Moon Kingdom) is still locked then the player cannot access the Moon Kingdom room
                if (rc.isLocked()) {
                    self.outputMessage("\nThis room is still locked. Please find the key to unlock.")
                    //currentRoom will not be changed to nextRoom
                    //Player will be located again in the same room
                    //***If the player uses the back command this room will be visited twice because they actually walked to the same room again because their location did not change**
                    self.outputMessage("\n\(currentRoom.description())")
                }
                    //else executes if nextRoom is the Moon Kingdom and it is NOT locked
                else {
                    //checks to see if the bag has all of the four inner Sailor Scout objects
                    if(self.hasAllObjects())
                    {
                        //the current song will stop playing and the win song will play
                        playThemeSong.musicHelper.stopAVPLayer()
                        playThemeSong.musicHelper.playWinningSong()
                        //Sets the currentRoom to nextRoom (Moon Kingdom)
                        self.currentRoom = nextRoom!
                        self.outputMessage("\n\(currentRoom.description())")
                        //winning prompt
                        self.outputMessage("\n\n\n\n\n\n\n\nI am the Princess and you have collected all the items. You Win!!!\nThank you for your help\n\nPlease quit to end the game.")
                        
                    }
                        //if nextRoom is the Moon Kingdom and it is NOT locked but the player did not win
                        //player can navigate to the Moon Kingdom like any other room and game play continues
                    else{
                        self.currentRoom = nextRoom!
                        self.outputMessage("\n\(currentRoom.description())")
                    }
                }
            }
                //if nextRoom is any room other than the Moon Kingdom
            else{
                self.currentRoom = nextRoom!
                self.outputMessage("\n\(currentRoom.description())")
            }
        }
            //if there is no room in that direction
        else {
            self.errorMessage("\nThere is no door on '\(direction)'")
        }
    }
    
    /*
     Function hasAllObjects() checks if the player's bag contains all four of the inner Sailor Scout objects
     @return bool, true if all 4 objects are in the bag
     returns false if the bag does not contain all 4 objects
     */
    func hasAllObjects() -> Bool {
        var objCounter = 0
        //loops through dictionary and checks the key names (which are also the object's names)
        //increments the counter by one each time a match is found
        for (key, _) in bag {
            if (key == "mercury") {
                objCounter += 1
            }
            if (key == "mars") {
                objCounter += 1
            }
            if (key == "jupiter") {
                objCounter += 1
            }
            if (key == "venus"){
                objCounter += 1
            }
        }
        //checks if the object counter is 4
        if objCounter == 4 {
            return true
        }
        else {
            return false
        }
    }
    
    /*
     Function amountOfObjects() returns the number of objects in the player's bag
     @return Int total, number of objects in bag
     */
    func amountOfObjects() -> Int {
        var total = 0
        for (_, _) in bag {
            //increments total for every entry in dictionary
            total += 1
        }
        return total
    }
    
    /*
     Function totalWeight() returns the total weight of items in the player's bag
     @return Int sum, total weight
     */
    func totalWeight() -> Int{
        var sum = 0
        for nameKey in bag.keys {
            //iterates through keys and adds the weight of the corresponding object to sum
            sum += (bag[nameKey]?.getWeight())!
        }
        return sum
    }
    
    /*
     Function give() is used to put an obect into the player's bag
     @param object, ScoutObject from the room
     */
    func give(object : ScoutObjects) {
        bag[object.getName()] = object
    }
    
    /*
     Function take() removes an object from the player's bag
     @param objName, String that is the name of the object to remove
     @return ScoutObjects, the corresponding object which may be nil
     */
    func take(objName : String) -> ScoutObjects? {
        //grabs the object with the same key as objName
        let object = bag[objName]
        
        //removes it from the bag if it is not nill
        if object != nil {
            bag.removeValueForKey(objName)
        }
        //the object is returned
        return object
    }
    
    /*
     Function dropAllItems() drops all objects in the player's bag into currentRoom
     Used with restart command
     */
    func dropAllItems() {
        for key in bag.keys{
            currentRoom.drop(bag[key]!)
        }
        bag.removeAll()
    }
    
    /*
     Function drop() takes an object out of the player's bag and drops it into the room
     @param objName, name of the object the player wants to drop
     */
    func drop(objName : String) {
        //takes the object out of the back and stores it in object variable
        let object = self.take(objName)
        
        //since take() can return a nil object, first check to see if it is nil
        if object != nil {
            //checks if the player is trying to drop the key
            //the key cannot be dropped unless the Moon Kingdom is currently unlocked
            if(objName == "key" && rc.isLocked() == false) {
                //drops the key into the currentRoom
                currentRoom.drop(object!)
                self.outputMessage("\nYou have dropped the key!")
            }
                //if the player is trying to drop the key but the Moon Kingdom is currently locked
                //will not let the player drop the key
            else if (objName == "key" && rc.isLocked()){
                //returns the object back to the player's bag
                self.give(object!)
                self.warningMessage("\nYou are unable to drop the key at this time!")
            }
                //if the player tries to drop any other object, there are no stipulations
            else{
                currentRoom.drop(object!)
                self.outputMessage("\nYou have dropped \(objName)'s Scout Object")
            }
        }
            //if the object is nil or not found, it cannot be dropped
        else {
            self.warningMessage("\nYou are unable to drop \(objName)")
        }
    }
    
    /*
     Function getObject() is used to get/pickup and object from the room
     @param objName, name of the object the player is trying to get
     */
    func getObject(objName : String){
        //gets the item from the room with the key value of objName and stores it in the variable object
        let object = currentRoom.pickUp(objName)
        
        //checks that the object is not nil and if adding it's weight to the current bags weight will be less than or equal to 7
        if (object != nil && ((object?.getWeight())! + self.totalWeight() <= 7)) {
            //puts the object in the player's bag
            self.give(object!)
            //if the object was the key a special prompt is printed since it's not a Scout Object
            if(objName == "key"){
                self.outputMessage("\nYou have collected the key!!")
            }
                //prompt printed for any other objects collected
            else{
                self.outputMessage("\nYou have collected \(objName)'s Scout Object!")
            }
        }
            //warning printed if the object is not found or if it is too heavy to be picked up/will exceed max weight of 7
        else {
            //returns that attempt that the player attempted to pick up back into the room
            currentRoom.drop(object!)
            self.warningMessage("\nYou are unable to collect \(objName)'s Scout Object")
        }
    }
    
    /*
     Function viewBag() displays the objects that the player has in their bag
     Prints the object name and weight
     */
    func viewBag(){
        //checks to make sure bag is not empy
        if(bag.count != 0){
            self.outputMessage("\nYou have the following items:\n")
            for (key, value) in bag{
                self.outputMessage("Item: \(key) - Weight: \(value.getWeight())\t")
            }
        }
            //if bag is empty
        else{
            self.outputMessage("\nYour bag does not contain any items")
        }
    }
    
    /*
     Function hasKey() checks to see if the bag contains the key
     Used for lockOrUnlock()
     @return bool, true if the bag has the key and false if it does not
     */
    func hasKey() -> Bool {
        for nameKey in bag.keys {
            if nameKey == "key" {
                return true
            }
        }
        return false
    }
    
    /*
     Funtion lockOrUnlock() is used to modify the status of the Moon Kingdom by using the Room Control object (rc)
     @param planet, location player is attemption to (un)lock
     */
    func lockOrUnlock(planet : String) {
        //checks if planet is moon
        //player can only manipulate the Moon Kingdom (moon entered for command)
        if planet == "moon" {
            //Player can only un(lock) Moon Kingdom from an adjacent room
            //Each if statement checks that the room is not nil and the room directly to the East, West, North, or South from the currentRoom is the Moon Kingdom
            //If this is true, and the player has the key in their bag the room is then (un)locked
            //the Lock() function changes the value of lock to it's opposite
            //Next a prompt is displayed telling the player if the room has been locked or unlock
            //***The player stays in the current room***
            if (currentRoom.getExit("east") != nil && self.hasKey() && currentRoom.getExit("east")!.getTag() == "Moon Kingdom") {
                //locks room
                rc.lock(currentRoom.getExit("east")!)
                //sees if the value is true or false
                if(rc.isLocked())
                {
                    self.outputMessage("\nYou have locked the Princess's Room!")
                }
                else {
                    self.outputMessage("\nYou have unlocked the Princess's Room!!")
                }
                self.outputMessage("\n\(currentRoom.description())")
            }
            else if (currentRoom.getExit("west") != nil && self.hasKey() && currentRoom.getExit("west")!.getTag() == "Moon Kingdom") {
                rc.lock(currentRoom.getExit("west")!)
                if(rc.isLocked()){
                    self.outputMessage("\nYou have locked the Princess's Room!")
                }
                else {
                    self.outputMessage("\nYou have unlocked the Princess's Room!!")
                }
                self.outputMessage("\n\(currentRoom.description())")
            }
            else if (currentRoom.getExit("north") != nil && self.hasKey() && currentRoom.getExit("north")!.getTag() == "Moon Kingdom") {
                rc.lock(currentRoom.getExit("north")!)
                if(rc.isLocked())
                {
                    self.outputMessage("\nYou have locked the Princess's Room!")
                }
                else {
                    self.outputMessage("\nYou have unlocked the Princess's Room!!")
                }
                self.outputMessage("\n\(currentRoom.description())")
            }
            else if (currentRoom.getExit("south") != nil && self.hasKey() && currentRoom.getExit("south")!.getTag() == "Moon Kingdom") {
                rc.lock(currentRoom.getExit("south")!)
                if(rc.isLocked()){
                    self.outputMessage("\nYou have locked the Princess's Room!")
                }
                else{
                    self.outputMessage("\nYou have unlocked the Princess's Room!!")
                }
                self.outputMessage("\n\(currentRoom.description())")
            }
            else {
                self.warningMessage("\nI'm afraid you can't unlock the Princess's Room from here")
            }
        }
            //if planet is any location other than moon
        else {
            self.warningMessage("\nThis room cannot be locked or unlocked")
        }
    }
    
    /*
     Function randomRoom() takes the player to a random room
     The room is changed from the currentRoom three times in a different direction
     */
    
    func randomRoom() {
        //array strings containing all of the directions
        var planetDirection2 : [String] = ["west", "east", "north", "south"]
        var randomInt = 0
        //for loop executes 3 times changing the room
        for _ in 0...2 {
            //a random integer is created between 0 and 3
            //this is used as in index for the direction array to get an direction
            randomInt = Int (arc4random_uniform(UInt32(4)))
            //checks that room in that direction is not nil and it is not the Moon Kingdom
            //if satisfactory, currentRoom is the new room
            if currentRoom.getExit(planetDirection2[randomInt]) != nil && currentRoom.getExit(planetDirection2[randomInt])?.getTag() != "Moon Kingdom" {
                currentRoom = currentRoom.getExit(planetDirection2[randomInt])!
            }
        }
        self.outputMessage("\n\(currentRoom.description())")
    }
    
    /*
     Function restart() restarts the game from the beginning
     */
    func restart() {
        //all objects in the player's bag are dropped
        self.dropAllItems()
        //prompt tells the player they have restarted and there are no items in their bag
        //all items are dropped in the current room and the player will have to pick them up from that room again
        self.outputMessage("\nYou have been awarded a fresh start!\nYou have found \(self.amountOfObjects()) items.")
        //the currentRoom is set to the first location in the tracker array which is home
        currentRoom = locationTracker[0]
        //all locations are removed from the tracker array
        locationTracker.removeAll()
        
        //if the Moon Kingdom was unlocked it is locked
        if(rc.isLocked() == false){
            rc.lockRestart()
        }
        self.outputMessage("\n\(currentRoom.description())")
    }
    
    /*
     Function askForItem() tells a player which object is located in the current room
     @param planet, the location of the room
     */
    func askForItem(planet : String) {
        //if player asks home
        if (planet == "home" && currentRoom.hasObject("key")){
            self.outputMessage("\nThis room contains the key")
        }
            //if player asks any other planet
        else if currentRoom.hasObject(planet){
            self.outputMessage("\n" + currentRoom.printObjects())
        }
            //if no object for that planet is found
        else {
            self.warningMessage("\nRoom and/or item not found")
        }
        
    }
    
    /*
     Funtion returnToRoom() returns the Room that was last visited and removes that location from the tracker array
     @return Room, the room last visited
     The value of this function is passed at the paramater for enterRoom when the back command is used
     */
    func returnToRoom() -> Room{
        //check that locationTracker is not empty
        if (locationTracker.count != 0) {
            previousRoom = locationTracker.last!
            locationTracker.removeAtIndex(locationTracker.count - 1)
        }
        else {
            self.errorMessage("\nYou cannot go back any further!")
        }
        return previousRoom
    }
    
    /*
     Function enterRoom() changes currentRoom to the previous room
     @param location, Room from returnToRoom() function
     */
    func enterRoom(location : Room) {
        //sets nextRoom to location
        let nextRoom : Room? = location
        //checks that is it not nil
        if nextRoom != nil {
            //changes the currentRoom to nextRoom
            self.currentRoom = nextRoom!
            self.outputMessage("\n\(nextRoom!.description())")
        }
            //if nil then the player cannot go back further
        else {
            self.errorMessage("\nYou cannot go back any further")
        }
    }
    
    /*
     Various message functions to change prompt colors
     */
    func outputMessage(message : String) {
        io.sendLine(message)
    }
    
    func outputMessage(message : String, color : NSColor) {
        let lastColor : NSColor = io.currentColor
        io.currentColor = color
        self.outputMessage(message)
        io.currentColor = lastColor
    }
    
    func errorMessage(message : String) {
        self.outputMessage(message, color: NSColor.redColor())
    }
    
    func warningMessage(message : String) {
        self.outputMessage(message, color: NSColor.orangeColor())
    }
    
    func commandMessage(message : String) {
        self.outputMessage(message, color: NSColor.brownColor())
    }
}
```
