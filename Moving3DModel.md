# Introduction

Add a moving 3D model in your scene.

## Add dragon prefab

- Add dragon into your scene (use the dragon prefab => comes from a 3D designer)
- if you play your scene the dragon is not moving in your scene


## Add material to your dragon
Select the prefab dragon from your assets folder and go to materials, so here you can add a new material

## Animations
you can preview to default animation from blender
- select the dragon prefab > go to animation tab > play the clip

- In your assets folder (where your dragon is stored), Create an animator controller > name it e.g. dragon_animator
- select the dragon game object in your scene
- unity added a Animator class to the game object
- add a controller
- select the dragon_animator

Now your dragon has the possibility to add animation. Right now, no animations are specified.
- open the dragon animator (select in your assets folder the animation > and click open animation)
- default: you have 3 states :
  - exit state: when your game object will be deleted, you go to exit state
  - entry state: when your game object is instantiated
  - any state: if you want to go from state1 to state2, you can add triggers. The any state controls this
  
 - add a new state (is in oranga: this means this is the default state)
 - every state has a motion (these are the animations clips coming from e.g. blender). Now you need to find the right animation 
 clip (coming from blender) => find the right clip => in our case it is flyinganimation)
 
 - don't forget to select the flyinganimation again, and check the loop time. So the animation will be play uninfinitely.
  
