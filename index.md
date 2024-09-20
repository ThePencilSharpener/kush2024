---
layout: base
title: This is my website. u better like it. or else 😈
description: Home Page
image: /images/mario_animation.png
---
<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages -->
{% include nav/home.html %}
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
define how HTML elements look 
--->
<style>

/*CSS style rules for the id and class of the sprite...
*/
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }
      }
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>




<p> 
Monkey bread is a delightful, sticky-sweet pastry that's as fun to make as it is to eat.
Originating from a recipe that combines chunks of dough with a gooey cinnamon-sugar mixture, it's baked in a bundt pan until golden and caramelized. 
The name "monkey bread" evokes the playful nature of the dish—it's meant to be pulled apart by hand, much like a monkey picking at a treat. The result is a rich, buttery treat with a crispy exterior and a soft, sugary interior that's perfect for breakfast, brunch, or even a decadent dessert. 
Each bite offers a burst of flavor and texture, making it a favorite for gatherings and special occasions.
</p>



<button type="button" class="dumb" onclick="window.location.href='http://127.0.0.1:4100/kush2024/mypage/';">Click here to go to my Journey page!!</button>

<style>
  .container {
            position: relative; /* Establishes a reference point for absolute positioning */
            height: 70px;  
        }
  .center {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(10%, -330%); /* Centers text */
        }
  .other {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(0%, -1900%); /* Centers text */
        }
  
  .dumb {
    background-color: red;
    color: white;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
  }
<body>
    <div class="container">
          <div class="center">I am a highly respectable young gentleman</div>
    </div>
</body>
</style>





<button type="button" class="dumb" onclick="window.location.href='https://cafedelites.com/chocolate-cake/'">Click here to go to a Chocolate cake recpie</button>



<button type="button" class="dumb" onclick="window.location.href='https://www.dmv.ca.gov/portal/file/california-driver-handbook-pdf'">Click here to go to a the DMV</button>


<p>
Monkeypox is a rare viral disease caused by the monkeypox virus, which belongs to the same family as the smallpox virus. First identified in laboratory monkeys in 1958, the disease primarily affects rodents but can also be transmitted to humans. Symptoms in humans often start with fever, headache, and muscle aches, followed by a distinctive rash that progresses through different stages. While monkeypox is generally less severe than smallpox, outbreaks can still pose significant public health challenges. The disease spreads through close contact with infected individuals or animals, and in recent years, there have been sporadic outbreaks in various parts of the world, prompting renewed attention and efforts to control its spread.
</p>



<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
.dropbtn {
  background-color: #04AA6D;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
}
.dropdown {
  position: relative;
  display: inline-block;
}
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f1f1f1;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}
.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}
.dropdown-content a:hover {background-color: #ddd;}
.dropdown:hover .dropdown-content {display: block;}
.dropdown:hover .dropbtn {background-color: #3e8e41;}
</style>
</head>
<body style="background-color:white;">

<h2>Check out this dropdown!</h2>
<p>Move the mouse over the button to open the dropdown menu.</p>

<div class="dropdown">
  <button class="dropbtn">Dropdown</button>
  <div class="dropdown-content">
    <a href="https://thepencilsharpener.github.io/kush2024/2024/09/10/github-playground-hack_IPYNB_2_.html">How I did this</a>
    <a href="https://thepencilsharpener.github.io/kush2024/javascriptcell/calculator">Javascript cell</a>
    <a href="https://thepencilsharpener.github.io/kush2024/2024/09/10/github-about-me_IPYNB_2_.html">About Me</a>
  </div>
</div>

</body>
</html>



<body>
  <div class="container">
    <div class="other">Salud</div>
  </div>
</body>

<img src="{{site.baseurl}}/images/IMG_2205.jpg" alt="Reading image" style="width:50%"/>


kefasgwejk fd