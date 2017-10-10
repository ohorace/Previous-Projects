## Olivia Horace  
## Final Project – Search for the Moon Princess  
  
I.	Game Description   
My game, Search for the Moon Princess, is based on the anime Sailor Moon. The player must navigate through the rooms of the Sailor Scouts and get the Sailor Scout objects from the four inner scouts. The inner scouts are Mercury, Mars, Jupiter, and Venus. Likewise, the player has to get the key and unlock the room where the Moon Princess is located. In order to win, the player must enter the Princess’s room with all four items from the inner Sailor Scouts.     
	
The player is able to: get items, drop the key, ask if there is an item that can be picked up, go to a random room, restart, and lock or unlock the Princess’s room. The player can go to different rooms, go back to previous rooms, and ask for help.  

II.	Game Play   
General game play shall be:  
-	The player starts from home   
-	The player can move room-to-room in any order  
-	In each room, the player can find out what objects are in that particular room  
-	The player can carry a max weight of 7  
o	The weights of objects are as follows: 
	* Mercury’s object – 1 
	* Mars’s object – 1
	* Jupiter’s object – 3
	* Venus’s object – 2
	* the Key – 2  
	
-	In order to carry the four items into the Princess’s room the player will have to drop the key  
-	The door of the Princess’s room must be unlocked using the key (the player does not automatically enter the room upon unlocking)  
-	There is no penalty for returning to a previously entered room  
-	If a player enters the Princess’s room and does not have all four Scout items, the game continues  
-	If a player enters the Princess’s room and has all four scout items, s/he wins  

III.	Commands I Created  
**Get:** get command allows the player to pick up an object. Only the objects of the inner planets and the key can be picked up. All other planets will not have an object that can be picked up.  
**Drop:** drop command allows the player to drop the key. Only the key can be dropped. As a result, the player has to strategize when to drop the key so the rest of the items can be picked up. Key can only be dropped if the Princess’s room is unlocked.  
**Ask:** ask command will let the player ask the planet they are in what Scout Object is in that room. The outer planets, Saturn, Neptune, Uranus, and Pluto, will have objects that cannot be picked up.  
**Random:** random command takes the player to a random room.  
**Restart:** restart command drops all items and takes player back to home  
**Lock:** lock command can either lock or unlock the Princess’s room. This room can only be locked or unlocked from an adjacent room.  

IV.	Implementation   
I built my game from the base code we were given. I added the ScoutObjects class for my objects. I used this class to keep track of the items a player has collected as well as functions related to these objects. The player class has a ‘bag’ object created from the ScoutObjects class to be able to use the methods in that class. The ScoutObject class contains the functions: hasObject, getObject, addItem, dropAllItems, dropKey, and objContained. 	 

Perhaps the most important implementation feature of this class is that the getObject func returns usable items for the inner scout planets and a dead item for the rest of the planets. This prevents the player from getting/picking up an object for any planet other than an inner planet. Instead of generically creating objects, I decided to use a function to create them because objects can also be deleted from the array of objects. My function allows them to be created again in case they are deleted.  
	
My go command executes the walkTo function where the current location is added to an array, locationTracker. This is done before the current location changes to the new room.  This array is used for the back command which executes the returnToRoom function. Here, the currentRoom is set to the value of the last index in the array (which is last location visited). I’m more comfortable with arrays in Swift than I am with stacks so that’s why I chose to use an array instead. 

For my random function I created an algorithm to change the room. In actuality, the random function is pseudo-random. I created an array of directions and used a random integer to point to an index in that array. Next, the function executes a for loop twice to move the room location in that same direction twice, provided that the direction points to an actual room and not nil.   
