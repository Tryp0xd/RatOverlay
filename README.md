# RatOverlay 1.0.0 - ChatTriggers QOL + Misc Module for Diana's Mythological Ritual

# Features
## Cheese Buff Timer
Cheese Buff Timer allows you to see how much time of the Rat Blessing is left whether you received it or you gave some to someone.
This allows you to see:
 - How many people buffed you
 - Coloured timers customizable to your liking (/ro -> Overlay)

![image](https://github.com/user-attachments/assets/22027931-3139-4ad0-a97c-b340a1168d75)

## Line and Box to Cheese ( ***USE AT YOUR OWN RISK*** ) 
This allows you to easily collect cheese as it draws a line to the cheese, and then draws a box on the cheese.
This may be considered a cheat as its ESP but I consider this a gray area as you can do debug show hitboxes and what you're really lacking is line to the cheese.

![image](https://github.com/user-attachments/assets/06a8d306-1ea8-42a9-8a3d-cfb0d7ce7599)

## Sound Alert
Plays a sound based on your desired interval in ticks. Default sound is `note.pling` but you can use [a list of sounds here](https://www.minecraftforum.net/forums/mapping-and-modding-java-edition/mapping-and-modding-tutorials/2213619-1-8-all-playsound-sound-arguments).
You cannot set the pitch or volume but if you so desire, you can always modify the code to your liking!

# Commands/How To Use

**/ro** -> Config  
**/romoveguis** -> Move GUI(s)  

***Debug Commands - To be removed**
**/roclearplayers** - Clears playerArr Array
**/rotestadd formattedName magicFind ticks type** - Adds a player to the playerArr array.
**/rogetoverlay** - Prints the structure of the overlays in /ct console js

Cheese buff timer works at all times, you collect the cheese and it lists the person, if you receive it lists who gave it to you.  
Line and box to cheese needs to be enabled through -> /ro | A race condition can happen where Hypixel hides other people's cheese but it can flash for a second causing the box to show up for a split second.  
Sound Alert can be enabled through -> /ro | If you put an incorrect sound then the thing will simply not work.

-------------------------------------------------------------

# Planned Features

## Kill Combo Tracker
### Features
  - Tracks your current chat kill combo (i.e. +15 Kill Combo! +3% Magic Find)
  - Tracks sum of buffs i.e. (+6% Magic Find, +20 coins, +15 Combat Wisdom)
  - Shows time left to Kill Combo expiring

Kill Combo Display (due to change at any moment and shows left alignment (explained later))

![image](https://github.com/user-attachments/assets/e0e51677-e08c-4859-9dac-146241079214)
 
### Discoveries while coding this
I basically found out that the Grandma Wolf kill combo duration is off by one index (i.e. where you see 10s, its actually 8s because its getting the value for the one below.

![image](https://github.com/user-attachments/assets/948344a9-6942-4cb1-81cf-9a80075ed073)

You can see that the durations go down from 10s to 3s, but did you know that this actually not the case?
After I made an extraction function that takes your Grandma Wolf stats and saves them for further use, I went to go and test the timer which after some time worked perfectly and got the starting time right... however! The times ended earlier than expected, I figured to test the times for each and they were literally the value below the intended combo.

| Combo | Intended duration | Actual duration |
| ----- | ----------------- | --------------- |
| 5 | 10s | 8s |
| 10 | 8s | 6s |
| 15 | 6s | 5s |
| 20 | 5s | 4s |
| 25 | 4s | 3s |
| 30 | 3s | 3s |
| 50 | 3s | 3s |

You can probably see the pattern and you can see what I mean by 'off by one index'. I reported this bug to Hypixel as this is probably an oversight and is definitely not intended. You know that one +15 Kill Combo you screwed up because you didn't kill the inq on time? That extra one second would have probably saved you then. Until this bug is confirmed to be fixed, I will still pull the incorrect data from the pet but adjust it to show the actual durations.

## Cheese Tally
### Features
  - Tallies the people you buffed with cheese
  - Tallies the people you got buffed by
  - Shows the amount and the percentage based on total

This is a written example of what it should look like:

---------------------------------------
Cheese Tally (Buffed by)

B3nSh4rk - 15 (75%)  
aquatol - 5 (25%)  

---------------------------------------
Cheese Tally (Given buff)

aquatol - 23 (76.7%)  
Vikesta - 4 (13.3%)  
Zxeky7 - 3 (10%)  

----------------------------------------

## Align text
### Features
  - just.. change the alignment of the overlay through settings, best example is the kill combo one.
