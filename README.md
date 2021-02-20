# Unity-ARFoundation-echoAR-demo-Portal-360Video
Simple portal demo with Unity, AR Foundation, and echoAR.

## Register
Don't have an API key? Make sure to register for FREE at [echoAR](https://console.echoar.xyz/#/auth/register).

## Setup
Follow the instructions on our [documentation page](https://docs.echoar.xyz/unity/adding-ar-capabilities) to [set your API key](https://docs.echoar.xyz/unity/adding-ar-capabilities#3-set-you-api-key).
* Clone this project and open the project in Unity.
* In the Portals folder, open up the Portal.unity scene (same as sample scene, but includes tags 'portal', 'portalVideo' and 'skyDome', and a box collider on the Main Camera).
* In Portal < Prefabs, drag portalController into the Hierarchy.
    * Click on portalController in the Hierarchy and drag SkyDome and PortalPlane into their respective fields in the Portal Controller script in the Inspector.
* Click the echoAR prefab and enter your API key.

## How to Create a Portal
1. Upload one of the portal models the [Models](https://github.com/echoARxyz/Portal-Demo/tree/master/Models) folder.
2. Add in the metadata from metadata.csv in the [Models](https://github.com/echoARxyz/Portal-Demo/tree/master/Models) folder.
3. Upload a 360 video to the console (e.g. 'Beach Sunrise' in the Portals folder).
4. In the uploaded video's metadata, assign it the key-value pair, 'name: "portalVideo"'.
3. At this point, the portal plane and skyDome will be created, the video will be projected on the inside of the skyDome, and you should be able to get a peek into the skyDome through the portal plane.
4. Going through the portal plane will unmask the rest of the video sphere, going back through the portal will mask it again.

## Run
Simply press the _Play_ button in Unity.

## Using Different Portal Models and Videos
* If you would like to use a portal model other than the one provided, you can upload it to the console and assign it the name 'portal' in the object's metadata. Just make sure there is only one named portal in the console!
* Similarly, if you would like to use a different portal video, you can upload it to the console and assign it the name 'portalVideo'.

## Adjusting the Portal Plane
* Since different models are configured in different ways, you may need to align or scale the portal plane with your model manually. There are a number of parameters for the portal plane that can be tweaked through its metadata.
* Translation: portalPlaneX, portalPlaneY, portalPlaneZ
* Rotation: portalPlaneXAngle, portalPlaneYAngle, portalPlaneZAngle
* Scale: portalPlaneScale

## Special Cases
* If a model and video are uploaded without "portal" or "portalVideo" names:
    Model and video plane just get instantiated as normal.
* If a model has a "portal" name, but there is no video with "portalVideo" name:
    A skyDome and portalPlane will be instantiated as children of the model, but the skyDome will not have a videoPlayer, until a "portalVideo" can be detected.
* If a video with a "portalVideo" name is found, but no model with a "portal" name:
    Video just gets displayed on a plane until a model with the "portal" name can be found.

## Notes
* The portal project relies on tags. Checks are made for models tagged as "portal" and "portalVideo" in order to be able to fuse these together to create the portal if both are present.
* The project works best if the portal model used is one with a gap or open space, such as an open door or window.
* Sometimes the model used as the portal may not have (0, 0, 0) as its origin (not aligned properly).

## Component Explanation
* Portal model: This could be an obj file of an open door, window, etc.
* portalPlane: This acts as the "window" into the portal (its material is what makes it act like a portal). The camera needs to go through this plane in order to enter the portal.
* skyDome: This is the large sphere that acts as the actual portal world. The 360 video is projected onto the inside of this sphere. It's hidden until the camera penetrates the portalPlane.
* portalVideo: This is just a VideoPlayer component that gets added to the skyDome once a video with the name "portalVideo" is added to the console.

## Known Bugs
- Sometimes the relative positioning between the portal model and portalPlane is flipped (suspected to be related to model alignment).
- Removing the "portalVideo" name from a video on the console will remove the VideoPlayer from the portal, but not instantiate a video plane again. Delete the video from the console and reupload it if you would like it to be on a video plane.

## Learn more
Refer to our [documentation](https://docs.echoar.xyz/unity/) to learn more about how to use Unity and echoAR.

## Support
Feel free to reach out at [support@echoAR.xyz](mailto:support@echoAR.xyz) or join our [support channel on Slack](https://join.slack.com/t/echoar/shared_invite/enQtNTg4NjI5NjM3OTc1LWU1M2M2MTNlNTM3NGY1YTUxYmY3ZDNjNTc3YjA5M2QyNGZiOTgzMjVmZWZmZmFjNGJjYTcxZjhhNzk3YjNhNjE).

## Screenshots
![console](/screenshots/console.jpg)
![additional data](/screenshots/additional%20data.jpg)
![portal](/screenshots/portal.gif)
