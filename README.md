This project deals with creating a realistic underwater environment, which includes water surface, light diffusion effects, and fog effects. We will not discuss underwater distortion as that will involve shaders, which fall out of the scope of this section.

This repo is based on the published paper:

```
@inproceedings{chaudhary_2021,
   author = {Akash Chaudhary and Rajat Mishra and Bharath Kalyan and Mandar Chitre},
   title = {Development of an Underwater Simulator using Unity3D and Robot Operating System},
   year = 2021,
   month = {Sep},
   publisher = {{IEEE}},
   booktitle = {{OCEANS} 2021 {MTS}/{IEEE}}
}
```


## Setting Up the Environment
We will first set up the environment using some simple shapes and Unity's Standard Assets. The steps are as follows:
1. Make a pool using 5 cubes by resizing them. 
2. Import Unity's Standard Assets from the Asset Store, into the project. 
3. Go to Standard Assets -> Environment -> Water
You'll see two options. Both are just different versions, and what you choose depends upon your preference and how much resources do you have to spare to render water. In this project, we use Water4Advanced. 
4. Further go to Water4 -> Prefabs and insert the **Water4Advance** into the scene. Resize it according to the size of your pool. 
*Note: Never scale it more than 2 times, or the waves will become choppy. Insert multiple instances of the prefab if you want to cover a larger area, each with a scale of 2 or lower.*
5. Set your camera (or cameras) at a good vantage position to observe the effects. You can have two cameras, one above the water and one below to better observe all the effects.
6. *Optional* Duplicate your water prefabs, rotate them 180 degrees on the x-axis and move them just a little bit below the original ones to get better reflections once you are underwater. 

***
![EX1](https://github.com/akash1306/UnderwaterExample/blob/master/Images/ex1.png)
***


Once this is done, we can now move on to add underwater fog to limit visibility. 

## Underwater Fog
Once the vehicle or player is underwater, it becomes very clear that the scene doesn't look realistic. It looks just like it does above water. So we will now add underwater fog. This is done by using unity's own Fog in the *Lightening Settings.* But before that, we will add a player which can move in the scene. 
1. Add a platform for the player to walk on, which is connected to the pool.
2. Add a capsule GameObject, which will behave as our body. 
3. Go to Standard Assets -> Characters -> FirstPersonCharacter -> Prefabs and add **RigidBodyFPSController** to the scene. Make it the parent of the Capsule that we added before, and make them overlap in position. 

This is our player now. You can playtest it by playing Ctrl + P and moving around in the scene, or even jump in the water. You can delete the cameras, although they can still be used for observations. 

4. Go to Window tab -> Rendering -> Lighting and click on the Environment Tab. You can see the Fog settings (under Other Settings) there. This is where we will set the color of our fog. (You can give colors to all other assets too, for aesthetic effects)
5. Check the box in front of the Fog option. This will switch on the fog. You will notice that the fog is greyish and it's everywhere, including above water. We will control its activation with a script. 
6. Change the mode to 'Linear', which gives it a more realistic effect. 
7. Keep the Start position as zero and set the end position according to your scene. I am using 20. 
8. Set the color according to your preference. I am using a dirty green color to get a more algae infested water body. 
9. Once you are satisfied with your fog color and distance, uncheck the fog check box. 

Now we will control it using a script. 

10. Import the Fogstart.cs script, from this project, into your project. 
11. Add this script to the camera component of the RigidbodyPlayer.
12. Insert the Water prefab in the water level Column of the script in the Inspector Panel of the Camera. 

This script checks whether the camera is underwater or not, and switches the fog on or off accordingly.  
***
![EX2](https://github.com/akash1306/UnderwaterExample/blob/master/Images/ex2.png)
***
Our fog is now in place, and we can now move forward with underwater light distortion effects. 

## Underwater Diffusion
When light passes through the water's surface, it diffuses and falls on the underwater surfaces in a continuously moving pattern. We will try to emulate this effect using caustics and projectors.
A Projector allows you to project a Material onto all objects that intersect its frustum. We will use two projectors. Once is a blob light projector and the other one is a grid projector. 
The BlobLight projector will project from the water's surface, while the grid projector will do it from above. 
1. Go to Standard Assets -> Effects -> Projectors -> Prefabs and add **BlobLightProjector** & **GridProjector** to the scene. Place the grid projector above the water surface, and the Blob light projector just below the surface. 
2. Import the WaterAnim.cs script from this project into your project and attach it to both the projectors. 
3. Import the Caustics folder to your projector, which contains the images that'll be projected onto the surfaces. 
4. Set the settings for the projectors in the inspector panel as shown below 

***
![EX3](https://github.com/akash1306/UnderwaterExample/blob/master/Images/ex3.png)
***

5. Add the images inside Caustics to the boxes under the script inspector panel of both the projectors. 

***
![Walkthrough](https://github.com/akash1306/UnderwaterExample/blob/master/Images/ex4.gif)
***

And that is how you create an underwater scene. You can insert several other objects in the scene according to your needs and create a custom controller for your player so that you can control it in all degrees of freedom when underwater.
