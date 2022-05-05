# Creating Mods
We are going to create some new mods for our game! The most practical way to do this is with XML files that are loaded in the `Mods` folder in the 7 Days to Die directory.   
This is because the devs have coded the game to actually read those files and change the game based on them, but there's a structure we must follow.   
By this point you should have Visual Studio Code open with a 'Config' folder in your workspace displaying all the `.xml` files in it.   
# File Structure
For the sake of simplicity we will have you make this on your Desktop.
+ Create a folder on your desktop called `MyMod`.
+ Inside this folder create a file named `ModInfo.xml`.
+ While still in the folder we made, create another folder called `Config`.   
+ Now drag the `MyMod` folder from your desktop into Visual Studio Code, click `Add To Workspace` and `Trust`.   
You should now have two folders in your workspace one is called 'Config' and the other is called 'MyMod'.

We need to setup the `ModInfo.xml` so the game will load your mod properly.
+ In the workspace under the 'MyMod' folder you should see `ModInfo.xml`, click on it.
Now add:

```xml
<?xml version="1.0" encoding="utf-8"?>
<xml>
	<ModInfo>
		<Name value = "MyMod Name Here"/>
		<Description value = "Description of my mod"/>
		<Author value = "My name"/>
		<Version value = "1.0"/>
	</ModInfo>
</xml>
```   
To fast copy the text, hover your mouse in the code box above and at the top right you will see a button, click it to copy!   

Of course you can edit the values you see fit.   
We are now ready to actually make the mod do something.
## Coding
We are going to make an example mod to show you how it's done.
+ Inside the workspace on vs code, under the 'MyMod' folder, click on the 'Config' folder, then right click and click `Add File`, name the file `blocks.xml`.   
+ Important: Any `.xml` file we are creating in the config is one that already exists by default in the game, the code we add to it will override the default one, but we have to name them the exact same also every `.xml` file we override must have:

```xml
<configs> <!--   <- This is the first line of the file.   -->
    
</configs> <!--  <- This is the last line of the file.   -->
```

+ Now in the `blocks.xml` inside the `<configs>` braces we are going to put:

```xml
    <!-- Eggs and feathers and honey from trees -->
	<append xpath="//block[@name='treeMaster']">
		<drop event="Destroy" name="foodHoney" count="1,5" prob="0.25"/>
		<drop count="2,6" prob="0.1" tag="allToolsHarvest" name="foodEgg" event="Harvest"/>
		<drop count="4,12" prob="0.1" tag="allToolsHarvest" name="resourceFeather" event="Harvest"/>
	</append>
```   
What does this code do? Well this code finds every tree and adds the chance for you to get Honey, Feathers, and Eggs when you chop down the tree.   

`This looks confusing and I don't understand any of it.`,  I completely get that, so let's explain it.

## Coding Explanation
The programming language used here is `XML`, which is a Markup Language. Markup languages such as XML and HTML are best described to help make code readable to humans and to computers.    
So let's disect exactly what's going on here line by line:

```xml 
<!-- Eggs and feathers and honey from trees --> 
```
Is whats known as a `comment`, it is basically something you write as a note to yourself in the code and will not be read by the game, it is ignored.

```xml 
<append xpath="//block[@name='treeMaster']">
```
Firstly, the `<append>` tag is a function in XML, a function is basically a command to do a predetermined task, the `append` task _adds_ to the end of a list of things,we'll get to that in a moment.    

Still on that line we also see `xpath="//block[@name='treeMaster']"`, 'xpath' is essentially another xml function that just looks for a specific thing in a specific directory.   

The `xpath=` will always be followed by double quotes, whats on this inside is the path or node.    

Next we have the `//`, these slashes like this are also like a function, that function is to jump into the file we are in and go through all of the different `braces` that look like '<>', anything inside these braces is another Node, the `//` looks through EVERY node until it finds one called `block`.    

So now we are at the `[@name='treeMaster']` part, the square brackets you should think of as `[Find a specific thing]`.   

Inside this bracket we have `@name='treeMaster'`, so, essentially it is looking for a `block` that has the name of `treeMaster`, all trees are connected to this `treeMaster` block.

Once the `xpath` has successfully found the thing you are looking for, in this case it is a specific Block named 'treeMaster', that xpath is now pointing at that block.

Now back to the `<append>` again, we are now pointing at that specific block, and since `append` we know adds something to the end of a list, we are going to add the chances for the items we want.

```xml
<drop event="Destroy" name="foodHoney" count="1,5" prob="0.25"/>
```
We are now adding a Node called `drop` to the bottom of the list of other nodes inside of the `treeMaster` block.   
`How do I know to add this 'drop' node??`, the 'drop' node is something that is already in the game and the game recognizes it as 'drop this thing' basically, to find more of these Nodes you would read the `blocks.xml` in the 7DTD Config folder where all the defaults are added and see what the other nodes are.

Now the `event="Destroy"` is an Attribute of a Node, the game recogizes this specific `event` attribute and then reads what the event is, in this case it's `Destroy`, again to know what attributes and events are used in the game, just read some of the Blocks in the `blocks.xml` so get a good idea of the ones you can use and how to use them.   

So now we know that this 'drop' node has an 'attribute' that is an 'event' called `Destroy`, meaning so far, this Node will make this block Drop something when it gets destroyed.  

Now the next part `name="foodHoney"` is the name of the Item it will drop when destroyed.   
Followed by that is `count="1,5" prob="0.25"` which means there is a 25% chance to have between 1 and 5 honey's dropped when the block is destroyed.


Now knowing all that we can disect the next two lines easier.

```xml
<drop count="2,6" prob="0.1" tag="allToolsHarvest" name="foodEgg" event="Harvest"/>
<drop count="4,12" prob="0.1" tag="allToolsHarvest" name="resourceFeather" event="Harvest"/>
```
So when this 'treeMaster' block has the 'event' of `Harvest` called, it will drop those items, but what is `tag="allToolsHarvest"` ?
The `tag` is basically just that to the game, it is something to Tag something else with for reference, in this case we have the `allToolsHarvest` tag which is for when you are Harvesting something.

So now! All in total we know what the code does: It appends the three nodes to the 'treeMaster' block, which we know connects to all the trees in the game, making it so that when you are harvesting any tree you have chances for eggs and feathers to fall, and once the tree falls it will have a chance to drop honey! 

## Other Questions
You probably have many other questions about `xpath` and `attributes` and Nodes and really just `xml` in general, and I can understand that.
I'll try to address a few here, but before that I would read this [website](https://www.w3schools.com/xml/xpath_intro.asp) that goes over it more.
+ 1: "How do I find the names of the other items?" Go read the `items.xml`.
+ 2: "I'm still confused, is there another way to learn?" Definitely check the link above.
+ 3: "I missed a step, is there a video I can watch?" Yes I made a video for this tutorial, you can view it [here](https://youtu.be/SVoVUxIhVRo). MaxFox also has some great tutorial [videos](https://youtu.be/-GOjiyAaPS0).
+ 4: "Can I message you if I need help?" Yes, of course don't abuse it, but I welcome anyone who wants to learn. (my discord is on the main page)
Before coming straight to me, please attempt to find the answer and definitely follow all of the steps first, thankyou!

## Done
You have now made a mod! Please continue to the next step.

[Back to Main Menu](../../main/README.md)

