```swift
//
//  RoomControl.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/20/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

/*
 Room Control class simply controls the lock on rooms.
 For my game, only the Moon Kingdom room uses this feature
 */
class RoomControl {
    //if lock is true, the room is locked
    //if lock is false, the room is unlocked
    var lock : Bool = true
    
    //Function returns the current status of the room
    //@return bool, lock status
    func isLocked() -> Bool {
        return lock
    }
    
    //Function locks the room (if it is the Moon Kingdom)
    func lock(room : Room) {
        if(room.getTag() == "Moon Kingdom") {
            //sets lock to the opposite value of what it is
            lock = !lock
        }
    }
    
    //Function locks the room in the case of the player restarting the game
    //Because the player can be in any room and restart it is simplier to take this command without a paramater
    func lockRestart(){
        lock = !lock
    }
}
```