# Tool Learning Log

## Tool: Godot

## Project: 2D Platforming Game

---

### 10/20/24:
* Went on [Youtube](https://www.youtube.com/watch?v=QKgTZWbwD1U&t=10s) to help me understand my tool
* I looked at [different](https://www.youtube.com/watch?v=UAS_pUTFA7o) [examples](https://godotengine.org/showcase/hive-time/) of what kind of style I want to make my game
* Next, I will try to make a 2D avatar of the main character for my game

### 11/2/24:
* Learned how to create a root of the scene using `Node2D`
* Learned how to display a 2D image using `Sprite`
* Going to try to learn how add color to the background

### 11/11/24:
* Learned how to create a root of the scene using `Node2D`
* Learned how to display a 2D image using `Sprite`
* Going to try to learn how add color to the background

### 11/17/24:
* Learned how to add color using `from_hsv` in the form of `Color.from_hsv(r: float, g: float, b: float, a: float)`
* Learned how to dim the background using `ColorRect` to apply a semi-transparent color
* Going to try to learn how to add depth to the background

### 12/1/24
* Learned how to use depth to certain backgrounds using `ParallaxLayer` nodes and set different `motion_scale` values for each `ParallaxLayer`
* Learned how to make shadows using `Light2D` and `LightOccluder2D` and added a texture to create a light source
* Going to try to learn how to make the screen shake when a certain action happens

### 12/8/24
* Learned how to make the screen shake by adding a `Camera2D` and setting its current property to `true` and by calling the `shake()` function
* Learned how change the intensity by using `shake_intensity` to make the shake stronger or weaker and `shake_duration` to control how long the screen will shake (ex: `$Camera2D.shake(10, 0.2)` The intensity is at 10 and lasts for 0.2 seconds)
* Going to try to learn how to make the screen border turn a different color

### 03/09/25
* Learned how to make a healthbar using `TextProgress` node as the root and then using `max_health` and `current_health` to set the current health
* Learned how to reduce/add to the health bar by using `current_health -= amount`/`current_health += amount` and then `max(current_health, 0)`/`min(current_health, max_health)` to make sure the health doesn't go past the max or go below 0
* Going to try to learn how make a stamina bar that decreases as you attack and slowly fills back up when not moving/attacking
<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
