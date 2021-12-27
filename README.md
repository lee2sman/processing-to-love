# From Processing (and p5.js) to Love

Notes and examples for getting started coding in [LÖVE](https://love2d.org/) aka Love aka Love2d for folks with previous experience in Processing, p5.js and the like.

### What is Love?

Love is a free, open source framework to make games in the Lua language and works on Mac, Windows, Linux, iOS, Android. There is a [wiki](https://love2d.org/wiki/Main_Page) with documentation, including a reference and a number of [additional libraries](https://love2d.org/wiki/Category:Libraries) and tutorials.

Just as p5.js is a library in Javascript and Processing is a framework in Java, Love is a framework built on top of the popular programming language Lua. Lua is about 30 years old, developed originally in Brazil, and noted for its speed, portability across operating systems, ease-of-use, and an emphasis on scripting as an extension language.

### Why use Love?

Although Love contains libraries like Processing for drawing to the screen Love is intended for the creation of games. It is particularly useful for making 2d games with tiles.

You may also want to try this out if you're interested in trying something new, learning a new language that is applicable to many other tools (Roblox, Playdate, Pico-8, Tic-80, and many more), and interested in a program that works fast and is cross-compatible on many computers. 

### Who makes Love?

Love is a programming language originally released in 2008. The developers are listed as Anjo, Bartbes, Rude, Slime, Vrld. The project is collaboratively managed on [GitHub](https://github.com/love2d/love) with additional contributions from dozens of other contributors.

### Download Love

Love can be downloaded from its [website](https://love2d.org/). Choose the download for your specific operating system.

## Creating and running your Love program

In p5.js, your sketch is generally a file called sketch.js. In Processing, your program is a custom file name you choose and ends in .pde.

In Processing, you may have coded in the Processing IDE. For p5.js you may have coded with the free online web editor. For Love, there is no special program for creating Love games. You can use any code editing program. If you have no previous experience, you could try installing [Atom](https://atom.io). Open up the preferences > install. Type in Language-lua and install the package that mentions that name. It will provide syntax highlighting to any file named and saved with a .lua extension.

In your desktop, command line or inside your code editor create a new folder for your game or program. In that folder you should name your program ```main.lua```. Other assets like images, fonts, sounds can be stored in the folder as well. 

There are multiple ways to run a love program. **The easiest way to run your program is to drop the whole folder containing your main.lua file and any other assets onto the Love application (also called an *executable* on Windows).** Some code editors will also be able to automatically run and launch love programs. For Linux and command line users, check out the [Getting Started](https://love2d.org/wiki/Getting_Started) for additional options of setting up and running Love programs or a list of code editors that can run Love directly.

### Hello World

Let's create a basic hello world program to test we're up and running.

Save this into your main.lua:

```
function love.draw()
  love.graphics.print('Hello World!', 400, 300)
end
```

Then drag and drop the *folder* holding this file (not the main.lua file itself) onto your Love application to launch it.

I'm on Linux running in the command line so to run this I can simply run ```love .``` inside that folder to launch it. (See the [getting started](https://love2d.org/wiki/Getting_Started) for more options)

### Default window size

Let's get some graphics onto the screen

In Processing, you may be aware there are hidden defaults. If you don't specify a ```size()``` then your sketch runs in a 100 by 100 pixel area. In p5.js, if you don't specify a size in ```createCanvas()``` then your sketch's canvas is also 100 by 100 pixels.

Since we didn't specify a size in our hello world program above it assumed a default window size of 800 by 600 pixels.  

### A More Processing-like first program

Let's get some shapes onto the screen.

In Processing and p5.js we might write a basic program like this:

```
//p5.js code
function draw(){
  rect(20,10,50,80);
}
```

In p5.js no setup means that a default canvas size of 100 by 100 will be created. No fill specified means the background will be white and the rectangle will have a black outline with white fill by default.

Let's write a similar program in Love.  You can erase the previous main.lua and try this

```
function love.draw()
    love.graphics.rectangle("fill", 20, 10, 50, 80)
end
```

Now save and run this program (drag the folder onto the Love application or run in the command line). If you have no errors you should see a black window 600 pixels wide by 800 pixels high with a white rectangle in the upper left corner. These colors and screen size are the defaults for Love.


### Basic structure of a Love program

In Processing and p5.js we usually have setup and draw functions. In Love, we have load, update and draw.

The function ```love.load()``` runs once when the program starts, similar to the setup function in Processing and p5.js.

The function ```love.update(dt)``` runs continously until our program ends. This is where we may call our own custom functions from, take input, or otherwise control our program. You may have noticed that update takes an argument *dt*. That stands for *delta time*. This is the number of seconds since the last time the update run. It is used to precisely calculate the exact amount of time and make adjustments, one of the things that makes Love particularly good for video games, where precision of time (for a clock, reaching a goal, physics, etc) is important.

Finally, ```love.draw()``` happens immediately after our update and this is where we draw any graphics to the screen. In Processing and p5.js these two functions are combined together but Love has us separate the two. **Graphics can only be drawn to the screen in draw**. In fact, as you've seen in our hello world example program, you can have a draw without a load or update, but without draw you won't be able to see anything on screen.

### A bite of syntax

To write a comment in Love, we put ```--``` at the beginning of the line.

```
-- This is a comment
```

Love (and Lua in general) does not use curly brackets to surround functions, conditionals and loops for example.

Instead of a curly bracket a function in Love ends with the word ```end```.

```
function myFunctionName(argument)
  -- function code in here
end
```

We can do multi-line comments in Lua, particularly useful for turning on and off sections of our code when we're debugging.

```
--[[
An example of a 
multi-line comment.
--]]
```

*You'll notice that most commands in Love start with ```love.```* This helps distinguish Love-specific functions from general Lua commands and your own custom written functions. It is a different approach from Processing or p5.js (for example, you don't have to write ```p5.ellipse(100,50,200,50);``` in p5.js.

### Working in color

In Processing or p5.js you can write ```fill(number)``` to specify a grayscale value. In Love you must specify all three R,G,B values. **Unlike Processing, in current version of Love color values must vary from 0 to 1 instead of 0 to 255.**

```
--to set a black fill
love.graphics.setColor(0,0,0)
```

An example:

```
function love.draw()
   --set to white
   love.graphics.setColor(1,1,1)
   love.graphics.print("This text is white but the below is red", 100, 100)
   
   --set to red
   love.graphics.setColor(1,0,0)
   love.graphics.print("This text is red", 100, 200)
end
```

To set a background color we use the clear command. This resets to a black transparent background, e.g. to the color (0,0,0,0).

```
function love.draw()
  love.graphics.clear()
end
```

If we want to specify a background color we can use R, G, B and set a transparency. 

To set a background color of green:

```
function love.draw()
  love.graphics.clear(0,1,0,1)
end
```

### other Shapes

Ellipse:

```
function love.draw()
  love.graphics.ellipse( mode, x, y, radiusx, radiusy, segments )
end
```

Unlike in Processing and p5.js you must specify the *mode*, either *fill* or *line*. In Processing and p5.js you specify the width and height. In Love you specify the radius (half of each of these). The segments is optional, the number of segments used to draw the ellipse.

Example ellipses:

```
function love.draw()
  love.graphics.ellipse("line",100,200,50,100,5)

  love.graphics.ellipse("line",300,200,50,100,30)
end
```

Run the program and notice the difference in how the ellipses are drawn based on the larger number of segments used in the second ellipse.

Example line:

```
function love.draw()
  love.graphics.line(100, 100, 200, 200)
end
```

Many additional shapes (triangle, quads, etc) can be created using the polygon function.

```
function love.draw()
  love.graphics.setColor(1,0,0)

  love.graphics.polygon("fill", 100,100, 200,100, 150,200)
end
```

More shapes can be found in the [drawing](https://love2d.org/wiki/love.graphics) section of the Love Wiki.

### Variables

Unlike Processing but similar to p5.js, you do not need to specify a variable's type.

**Unlike Processing and p5.js, all variables are global, even those created inside functions, unless specified as local-only**.

Javascript and Java have the ++ shortcut, known as *syntactic sugar* to increment a variable. Lua does not.

```
function love.load()
    x = 0 
end

function love.update(dt)
  x=x+1
end

function love.draw()
  love.graphics.setBackgroundColor(0,0,0,0)
  love.graphics.setColor(1,0,0)
  love.graphics.print("x: "..x, 100, 200)
end
```

### Example of motion

```
-- example moving a shape on screen
function love.load()
    x = 100 
end

function love.update()
  x=x+1
end

function love.draw()
    love.graphics.rectangle("fill", x, 50, 200, 150)
end
```

### Using the mouse

In Processing and p5.js we are used to the mouseX and mouseY built-in variables for getting the location of the mouse's X and Y coordinates.

Love provides the getX() and getY() functions.

```
function love.draw()
  --move mouse on screen to see result
  local x = love.mouse.getX()
  love.graphics.line(x,0, x,love.graphics.getHeight())
end
```

### Example demonstrating keypressed function, conditionals and random number generation and Love syntax

In this example pressing a space key down stores a random number between 100 and 500 in the variable num.

```
function love.keypressed(key)
    --If space is pressed then..
    if key == "space" then
        num = math.random(100, 500)
    end
end
```

### Drawing Images to screen

Like Processing and p5.js, Love has functionality built in to easily import images.

We load an image to a variable using love.graphics.newImage() in the love.load() function. We draw it to the screen using love.graphics.draw() in the love.draw() function.

Images are objects, so we can optionally use :getWidth() and :getHeight().

**The color of an image is affected by any previous setColor() command**.

```
function love.load()
  img = love.graphics.newImage("sloth.jpg") 
  -- make cursor invisible
  love.mouse.setVisible(false)
end

function love.draw()
  -- get mouse coordinates
  local x, y = love.mouse.getPosition() 

  --draw img centered on mouse's coordinates
  love.graphics.draw(img, x - img:getWidth()/2, y - img:getHeight()/2) 
end
```

### More differences from Processing (Java) and p5.js (Javascript)

To combine strings, we use the .. syntax.

In p5.js:
```
text("My name is "+name,50,50);
```

In Love:
````
love.graphics.print("My name is "..name, 50, 50)
```

### To distribute programs

When you're ready to distribute your program you will zip up the folder and rename the extension .zip to .love to create an executable Windows exe file, a Mac App, or Linux AppImage. [additional info](https://love2d.org/wiki/Game_Distribution#Create_a_.love-file)


### Built-in functionality in Love

* [Physics](https://love2d.org/wiki/love.physics)
* [Collision detections](https://love2d.org/wiki/Tutorial:PhysicsCollisionCallbacks)  
* [Joystick support](https://love2d.org/wiki/love.joystick)
* Access to the [operating system](https://love2d.org/wiki/love.system) and [file system](https://love2d.org/wiki/love.filesystem) 
* [Video](https://love2d.org/wiki/love.video)
* [Audio](https://love2d.org/wiki/love.audio)
* [Fullscreen](https://love2d.org/wiki/love.window.setFullscreen)
* [Packaging programs for distribution](https://love2d.org/wiki/Game_Distribution)

### Resources

* [Love Wiki](https://love2d.org/wiki/Main_Page) - contains the reference, tutorials, etc
* [Love Forums](https://love2d.org/forums/) 
* [Love Discord server](https://discord.com/invite/rhUets9)  
* [Awesome Love](https://github.com/love2d-community/awesome-love2d) - "A categorized community-driven collection of high-quality, awesome LÖVE libraries, projects, and resources."
* [Obey_love](https://twitter.com/obey_love) official Twitter account of Love
* Tutorial on setting up Love in [Visual Studio Code](https://twitter.com/obey_love) 


### Tutorials
* [How to Love](https://sheepolution.com/learn/book/contents) comprehensive and beginner-friendly book on Love by Sheepolution 
* [Conditionals](https://sheepolution.com/learn/book/6), [Tables and For-Loops](https://sheepolution.com/learn/book/7), [Classes](https://sheepolution.com/learn/book/11) from How To Love
* [Falling in Love with Lua](https://www.youtube.com/watch?v=3k4CMAaNCuk) YouTube video and [slides](https://docs.google.com/presentation/d/1K3GN5827gbqQZJzKu43kXPaW2cTkJWja8WWbrv2Wnmc/edit#slide=id.p), a tutorial on building a basic procedurally generated version of Mario in Love
* Basic [Physics tutorial](https://love2d.org/wiki/Tutorial:Physics)
* Love [Tile Tutorial](https://github.com/kikito/love-tile-tutorial/wiki) to make  tile-based game

# License

This tutorial is Public Domain under The Unlicense except where any code examples from Love are used, under the GNU Free Documentation License 1.3.
