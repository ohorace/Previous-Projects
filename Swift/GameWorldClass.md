```swift
//
//  Game World.swift
//  Final_OliviaHorace
//
//  Created by Olivia Horace on 7/13/16.
//  Copyright © 2016 Rodrigo Obando. All rights reserved.
//

import Foundation

class GameWorld {
    //by using '?' entrance can be nil so the initializer can call the createWorld method using self
    var entrance : Room?
    static var sharedInstance = GameWorld()
    
    private init(){
        //creates a world
        entrance = createWorld()
    }
    
    func createWorld() -> Room {
        //Creates rooms and sets exits
        let home = Room(tag: "Home")
        let mercury = Room(tag: "Planet Mercury")
        let venus = Room(tag: "Planet Venus")
        let earth = Room(tag: "Planet Earth")
        let mars = Room(tag: "Planet Mars")
        let jupiter = Room(tag: "Planet Jupiter")
        let saturn = Room(tag: "Planet Saturn")
        let uranus = Room(tag: "Planet Uranus")
        let neptune = Room(tag: "Planet Neptune")
        let pluto = Room(tag: "Planet Pluto")
        let moon = Room(tag: "Moon Kingdom")
        
        home.setExit("north", room: pluto)
        home.setExit("south", room: mercury)
        home.setExit("east", room: earth)
        home.setExit("west", room: moon)
        
        mercury.setExit("west", room: mars)
        mercury.setExit("north", room: home)
        mercury.setExit("south", room: neptune)
        
        venus.setExit("west", room: saturn)
        venus.setExit("south", room: earth)
        
        earth.setExit("west", room: home)
        earth.setExit("north", room: venus)
        earth.setExit("south", room: jupiter)
        
        mars.setExit("north", room: moon)
        mars.setExit("east", room: mercury)
        
        jupiter.setExit("north", room: earth)
        jupiter.setExit("west", room: neptune)
        
        saturn.setExit("south", room: pluto)
        saturn.setExit("west", room: uranus)
        saturn.setExit("east", room: venus)
        
        uranus.setExit("south", room: moon)
        uranus.setExit("east", room: saturn)
        
        neptune.setExit("north", room: mercury)
        neptune.setExit("east", room: jupiter)
        
        pluto.setExit("north", room: saturn)
        pluto.setExit("south", room: home)
        
        moon.setExit("north", room: uranus)
        moon.setExit("south", room: mars)
        moon.setExit("east", room: home)
        
        
        /*
         Creates objects that correspond with each room
         Drops each object into it's room
         */
        let homeObject : ScoutObjects = ScoutObjects(newItem: "key", newWeight: 2)
        home.drop(homeObject)
        
        let mercObject : ScoutObjects = ScoutObjects(newItem: "mercury", newWeight: 1)
        mercury.drop(mercObject)
        
        let marsObject : ScoutObjects = ScoutObjects(newItem: "mars", newWeight: 1)
        mars.drop(marsObject)
        
        let juptObject : ScoutObjects = ScoutObjects(newItem: "jupiter", newWeight: 3)
        jupiter.drop(juptObject)
        
        let venusObject : ScoutObjects = ScoutObjects(newItem: "venus", newWeight: 2)
        venus.drop(venusObject)
        
        let satuObject : ScoutObjects = ScoutObjects(newItem: "saturn", newWeight: 8)
        saturn.drop(satuObject)
        
        let neptObject : ScoutObjects = ScoutObjects(newItem: "neptune", newWeight: 8)
        neptune.drop(neptObject)
        
        let uranObject : ScoutObjects = ScoutObjects(newItem: "uranus", newWeight: 8)
        uranus.drop(uranObject)
        
        let plutoObject : ScoutObjects = ScoutObjects(newItem: "pluto", newWeight: 8)
        pluto.drop(plutoObject)
        
        let earthObject : ScoutObjects = ScoutObjects(newItem: "earth", newWeight: 8)
        earth.drop(earthObject)
        
        //returns the home room as the starting point
        return home
    }
}
```