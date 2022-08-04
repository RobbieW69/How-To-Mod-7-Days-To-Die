# Modding XML Files
The XML files contain alot of the configurations/settings the game runs on, so changing them to what we want is called modding.
Modding the games default XML files directly is ineffecient as when the game updates, any XML's that were changed will be replaced once again by the new updated game files. As such The Fun Pimps allows us to indirectly edit those files from a Mods folder, so when the game updates we don't lose all of our hard work.
# Syntax/Format
XML's syntax is a tree of nodes style structure, each node can contain different attributes. 
+ Nodes are anything within a pair of `< > </>`.
  + The first Node is the main Node or Parent node.
  + Any nodes within a node are called Child nodes, I call them Sub nodes.
For example:
```xml
<?xml version="1.0" encoding="UTF-8"?>

<bookstore>
  
  <book category="cooking">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  
</bookstore>
```
In this example XML file, we have the Main node or Parent node called "bookstore", with another node called "book", now book has an Attribute, an attribute is just a reference about something, the attribute it has is "category".   
Now within that "book" node we have more sub nodes, Title, Author, Year, Price, ect. You might be asking why not just give them those as attributes instead of making them sub nodes? Well the answer is effeciency, in this manner we can use XPATH in order to change many things all at once.
# Xpath
XPATH is a syntax in XML to navigate xml files and when used with expressions and functions allows you to do alot of different things. We will be using this to make those indirect modifications to the games default XML files!
## Expressions in XPATH
Expressions in Xpath are how we get the xpath to "look" / navigate through the xml. There are many different expressions that do many things. Just remember once you get used to using the expressions you'll realize that XPATH just "points" or "grabs a hold of" the specific node/attribute you direct it toward.
Here is a list of expressions and what they do:
| Expression  | Description |
| ------------- | ------------- |
| /  | Goes into the Main node, or root node.  |
| //  | Finds any node within the document  |
| .  | Selects the current node.  |
| ..  | Selects the parent of the current node.  |
| @  | Selects an attribute.  |      

Here's some examples of these using our Bookstore xml.
```xml
xpath="/bookstore" <!-- Goes into the main node -->
xpath="//book" <!-- Finds any Book node -->
xpath="//book[@category='cooking']/." <!-- Selects Book -->
xpath="//book[@category='cooking']/.." <!-- Selects Bookstore -->
xpath="//book/@category" <!-- Selects the 'category' attribute -->
```
## Functions in XPATH
Functions are similar to expressions in the sense that they are preprogrammed to do something, using the different functions is in relation to what you are trying to do.
For example if you wanted to find a book node where the category is cooking and not cleaning it would like this.
```xml
xpath="//book[@category='cooking' and not(@category='cleaning')]"
```
In this example the function is `not()` which determines if the things inside are not equal. The `and` is an operator.
## Commands in Xpath
There are "function" like commands in xpath that look like nodes, in essence they are nodes that are predetermined to do something specific.
Here is a list of the ones I currently have used:
| Command  | Description |
| ------------- | ------------- |
| set  | Sets a node or attribute.  |
| setattribute  | Sets an attribute only.  |
| remove  | Removes a node or attribue.  |
| removeattribute  | Removes an attribute only.  |
| append  | Appends code to the bottom of a list of things. (ie. Nodes)  |    

Here's some examples using our bookstore once again:
```xml
<!-- Finds the book, selects the Price node, sets it to 50$ instead of 30 -->
<set xpath="//book[@category='cooking']/@price">50.00</set>    
```
```xml
<!-- Sets the 'category' attribute to 'cleaning'-->
<setattribute xpath="//book[@category='cooking']" category="cooking">cleaning</setattribute>    
```
```xml
<!-- Removes the whole node -->
<remove xpath="//book[@category='cleaning']"/>    
```
```xml
<!-- Removes the 'category' attribute -->
<removeattribute xpath="//book[@category='cleaning']/@category"/>    
```

```xml
<!-- Adds a new Book node to the main node -->
<append xpath="/bookstore"> 
  <book category="coding">
    <title lang="en">C# for dummies</title>
    <author>RobbieW</author>
    <year>2022</year>
    <price>5.00</price>
  </book>
</append> 
```

## Operators in XPATH
Operators are operands like + or > ect, these operands tell the the code what to do.
The operators we can currently use are;     
| Operator  | Description | Example |
| ------------- | ------------- | ------------- |
| +  | Addition  | 2 + 2  |
| -  | Subtraction  | 2 - 1  |
| *  | Multiplication  | 3 * 3  |
| =  | Determines whether two things are equal.  | @name='meleeToolTorch'  |
| != | Determines whether two things are NOT equal.  | @name != 'treeStump'  |
| <  | Less than | @count < '5'  |
| <= | Less than or equal to | @count <= '5'  |
| >  | Greater than | @count > '5' |
| >= | Greater than or equal to | @count >= '5'  |
| or | Selects one thing OR another | @name='meleeToolTorch' or @name='meleeToolFlashlight02' |
| and | Selects something AND something else | @name='gunMGT1AK47' and @count='100' |
| mod | The modulus (division remainder) | 5 mod 2 |

