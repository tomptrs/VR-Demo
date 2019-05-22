## Introduction

remove standard camera
Add SteamVR plugin (via asset store)
Add into your scene: steamvr > core >Prefabs > Player or camerarig

(=> difference: camerarig has 2 trackers, with player you have much more functionality available. Tip: use player if you have 
interaction with objects)

## Setup interaction with Vr

- go to window > steam vr input > steamvr input (you are making basic files for actions)
You can adapt the actions, but for now it's ok to push save and generate (you have to do this once!)

In your assets folder you have a steamvr_input folder > if you generate your actons: unity creates a class with
getters for the actions (steam_vr Input > actionsetclasses)

### test the interactivity

window > steamvr input live view

(don't forget to start your scene)

## Script to grab a cube

- add cube to scene

- go to steam_vr > interactionsystem > core > scripts > Throwable
-  the throwable scripts also adds other scripts: e.g. interactable script: This is a script from steamvr: it has implemented a collision detection between controller and cube (and it will glow the cube) => 
so your transform of your controller is relative

- add throwable script to cube
=> in your inspector you can change some properties about the interaction


=> now because you added the throwable script, your cube has a rigidbody (the fysics from unity), so it adds gravity to your object. If you
start the application, your cube will fall. To prevent this you need to add a plane to your scene (without a rigidbody), so your 
object will nog fall anymore.
