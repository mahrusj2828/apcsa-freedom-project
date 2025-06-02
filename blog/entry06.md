# Entry 6
##### 05/31/25

* After months of development in Godot, I've completed my 2D action-adventure game prototype with fun combat mechanics, responsive enemy AI, and a rewarding character progression system. The journey from concept to playable prototype has been educational, teaching me about the importance of game architecture, the importance of clean code organization, and the way in which subtle design choices influence player experience. Through a repetitive process of testing and iteration, I've created a system that combines responsive, tight controls with simple combat depth. The player controller itself went through many iterations before landing on its present state-based methodology, which now incorporates directional attacks (side, front, back) and smooth animation transitions. Another of my greatest breakthroughs was appropriately separating the movement logic from the animation control, which rendered the code not only easier to maintain but also enabled combat responses and character feedback to be smoother.

``` gdscript
extends CharacterBody2D

var enemy_inattack_range = false
var enemy_attack_cooldown = true
var health = 150
var player_alive = true
var attack_ip = false
const speed = 100
var current_dir = "down"

func _physics_process(delta):
    player_movement(delta)
    enemy_attack()
    attack()

    if health <= 0:
        handle_player_death()

func player_movement(delta):
    velocity = Vector2.ZERO

    if Input.is_action_pressed("ui_right"):
        current_dir = "right"
        play_anim(1)
        velocity.x = speed
    elif Input.is_action_pressed("ui_left"):
        current_dir = "left"
        play_anim(1)
        velocity.x = -speed
    elif Input.is_action_pressed("ui_down"):
        current_dir = "down"
        play_anim(1)
        velocity.y = speed
    elif Input.is_action_pressed("ui_up"):
        current_dir = "up"
        play_anim(1)
        velocity.y = -speed
    else:
        play_anim(0)

    move_and_slide()
```

* The enemy AI was created through several iterations to achieve the best balance between difficulty and fairness. The completed version features intelligent pathfinding with obstacle adjustments, dynamic knockback reactions that allow for feeling impactful during combat, and optimally tuned attack cooldowns to prevent frustration. The system uses a state machine design for seamless transitions between idle, chase, and attack states, based on distance limits to prevent endless pursuit. These features create intelligent-feeling opponents that are aimed to never feel unbalanced.

``` gdscript
extends CharacterBody2D

var speed = 50
var player_chase = false
var player = null
var health = 80
var player_inattack_zone = false
var can_take_damage = true

func _physics_process(delta):
    deal_with_damage()

    if player_chase and player != null:
        direction = (player.position - position).normalized()
        velocity = direction * speed
        move_and_slide()
        update_animation()

func deal_with_damage():
    if player_inattack_zone and Global.player_current_attack:
        if can_take_damage:
            health -= 20
            $take_damage_cooldown.start()
            can_take_damage = false

            # Knockback effect
            if player != null:
                var knockback_direction = (position - player.position).normalized()
                velocity = knockback_direction * (speed * 3)
                move_and_slide()

            if health <= 0:
                self.queue_free()
```

* I implemented a global state system to manage combat flags and game-wide variables, which proved essential for coordinating between different game systems.

``` gdscript
extends Node

var player_current_attack = false
```

* While finalizing this project, I’ve been focusing on the "Attention to Detail" skill. It’s an important skill for me because it helps me make sure that my code is clean, my animations are seamless, and every gameplay interaction works as intended. It helps me catch bugs and polish rough edges, turning a functional prototype into a professional-quality game. Another important skill I’ve practiced is "Creativity". It is an important skill to learn because it pushes me to think outside conventional solutions, whether designing dynamic knockback effects or optimizing AI behavior. These skills don’t just improve the game; they help me grow as a developer who can solve problems in ways players will remember.

[Previous](entry05.md) | [Next](entry07.md)

[Home](../README.md)