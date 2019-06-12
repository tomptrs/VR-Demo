# Soft Cuts

## introduction

If you only want to look around, you don't have to remove the main camera, but in Project settings > Player Settings > XR Settings => enable 
virtual reality supported

If you need interaction, you have to install the steamvr plugin:
remove standard camera Add SteamVR plugin (via asset store) Add into your scene: steamvr > core >Prefabs > Player or camerarig
(=> difference: camerarig has 2 trackers, with player you have much more functionality available. Tip: use player if you have interaction with objects)


## Project

### Drag videos in unity assets

Unity step-by-step plan for integrating your 360 movies:

1. Create a new material (right mouse button scene> create material)
>The settings are: shader: skybox / Panaramic

2. Create a new texture (the dimensions are the same as those of your recorded film (= 3840x2160)
3. Go back to your material and drag your texture into it
4. Create a video player in your scene, and add your video + drag your texture to the video player (enable loop in video player)
5. Go to windows> rendering> lighting settings and the skybox material must now be your self-made material.
Play your unity scene. or  you drag your skybox material in your scene

### Sensitivity Angle

Our candle light is at Y-axis: 69°. The opposity angle = 69+180 = 249°
Let's make a sensitivity parameter of 180° . This means if the viewer looks in the oppossite direction of the candle light the 
Y-rotation is between 159° (=249-90) and 339° (249+90). (why 90 => 90+90 = 180, and this is our sensitivity parameter.

1. Create an empty object (e.g. videoclipmanager)
2. Assign a c# script to our empty object with the name videoclipmanager:VCM)

```

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Video;

public class VideoClipManager : MonoBehaviour
{
    public Transform Head; //Assign Camera-transfrom of [CameraRig] Object via the scene

    public float AngleSenstivity; //If you want to make a slider of this parameter: https://docs.unity3d.com/ScriptReference/EditorGUI.IntSlider.html

    public float ViewAngle; //Angle of the object over Y-Axis you want to change.

    /*
     * Variable needed to change the videoclip, assign videoplayer, videoclip from the scene.
     */
    public VideoPlayer VideoPlayer;
    public VideoClip VideoClip;

    private float minAngle, maxAngle;

    // Start is called before the first frame update
    void Start()
    {
        //Define min & max angles of interval
        minAngle = ViewAngle + 180f - AngleSenstivity;
        maxAngle = ViewAngle + 180f + AngleSenstivity;     
    }

    // Update is called once per frame
    void Update()
    {
        if(Head.transform.rotation.eulerAngles.y >= minAngle && Head.transform.rotation.eulerAngles.y <= maxAngle)
        {
            VideoPlayer.clip = VideoClip;
        }
        
    }
}


``` 

You need to garantuee you see the first clip, so in our update method we have to write extra code to check we saw clip 1. 
We can do this with an extra boolean hasSeen.

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Video;

public class VideoClipManager : MonoBehaviour
{
    public Transform Head; //Assign Camera-transfrom of [CameraRig] Object via the scene

    public float AngleSenstivity; //If you want to make a slider of this parameter: https://docs.unity3d.com/ScriptReference/EditorGUI.IntSlider.html

    public float ViewAngle; //Angle of the object over Y-Axis you want to change.

    /*
     * Variable needed to change the videoclip, assign videoplayer, videoclip from the scene.
     */
    public VideoPlayer VideoPlayer;
    public VideoClip VideoClip;

    private float minAngle, maxAngle;
    private bool HasSeen = false;

    // Start is called before the first frame update
    void Start()
    {
        //Define min & max angles of interval
        minAngle = ViewAngle + 180f - AngleSenstivity;
        maxAngle = ViewAngle + 180f + AngleSenstivity;     
    }

    // Update is called once per frame
    void Update()
    {
        if (Head.transform.rotation.eulerAngles.y >= ViewAngle - 20 && Head.transform.rotation.eulerAngles.y <= ViewAngle + 20)
        {
            HasSeen = true;
        }
        else if (Head.transform.rotation.eulerAngles.y >= minAngle && Head.transform.rotation.eulerAngles.y <= maxAngle && HasSeen)
        {
            VideoPlayer.clip = VideoClip;
        }
    }
}


```


 
