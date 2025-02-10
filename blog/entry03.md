# Entry 3
##### 02/09/25

* I am still experimenting with [Godot](https://godotengine.org), a free open-source game engine that allows you to develop your own 2D & 3D or even cross-platform games using C++, C# or GDScript. With Godot, I want to make a 2D RPG based game where you could build you own character and I have been using GDScript to code and make the game. Over the course of nearly a month, I have been trying to add more to what I previously had and work on a little more on the character design aspect of the project. I wanted to create a character that was able to move and is able to attack based on commands/inputs given by the user. I looked at different [tutorials](https://www.youtube.com/watch?v=NVAXjTzqTyE) on [Youtube](https://www.youtube.com/watch?v=rUE9gA8OltA) to help me figure out how to try and make my character move and attack. I had to create a code that was inside the `_process(delta)` function which listens for the "attack" action input. If the player presses the attack button and `can_attack` is true, it calls the `attack()` function.

``` GDScript
if Input.is_action_just_pressed("attack") and can_attack:
    attack()
```

* However, the actual attack logic is handled in the `attack()` function where it plays the attack animation using `sprite.play("attack")` where a cooldown starts to prevent immediate re-attacks by `setting can_attack = false` to disable further attacks.

``` GDScript
    func attack():
        can_attack = false
        sprite.play("attack")
        print("Player attacked!")  # Replace with attack logic
        attack_timer.start()
```

* To trigger the cooldown, I had to use the `_on_attack_timer_timeout()` element where once the cooldown timer ends, `can_attack` is set to true, allowing another attack.

``` GDScript
    func _on_attack_timer_timeout():
    can_attack = true
```

* However, to even be able to make the character move at all, I had to the `extends Character2D` element where `CharacterBody2D` provides physics-based movement, including functions like `move_and_slide()`. I also needed to declare how fast the character is moving by using `@export var speed: float = (value)`. To call every frame to update player movement, I needed to use `handle_movement(delta)`.

``` GDScript
func _process(delta):
    handle_movement(delta)

    if Input.is_action_just_pressed("attack") and can_attack:
        attack()
```

* To get the player moving, I had to use the `direction` element which stores movement input as a `Vector2` and to get input values for movement keys `ui_right`, `ui_left`, `ui_down`, `ui_up`, I needed to use `get_action_strength()`.

``` GDScript
func handle_movement(delta):
    var direction = Vector2.ZERO
    direction.x = Input.get_action_strength("ui_right") - Input.get_action_strength("ui_left")
    direction.y = Input.get_action_strength("ui_down") - Input.get_action_strength("ui_up")
```

* I will continue to experiment to see how I can make different animations based on if the character is moving or if the charctor is stationary/idle. I also want to try to see and make it so that the character's movement speed changes based on how hard or light you press a direction key.

* For this blog entry, I am currently on the Creating a Prototype part of the Engineering Design Process (EDP) where I am using different elements that I have learned so far in Godot to try to make a smooth game that people would like to play. I think I will continue to be in the Creating a Prototype part of the process because there are still things that I want to try to make before refining my game. While working on this blog, I have been working on the skill "Growth Mindset". This is an important skill for me to learn because I need to be patient when trying to figure out what elements work in different situations and how I can try to improve. Another important skill for me to learn is "How to Google". This is another important skill to learn because you might not remember how to do a certain thing and might need some assistance from the internet to help or if you want to try out something new that you might think would benefit the thing that you want to do.

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)