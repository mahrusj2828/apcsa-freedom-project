# Entry 6
##### 05/31/25

* After months of development in [Godot](https://godotengine.org) using [different](https://www.youtube.com/watch?v=LOhfqjmasi0&t=178s) [Youtube](https://www.youtube.com/watch?v=mAbG8Oi-SvQ&list=PL9FzW-m48fn2SlrW0KoLT4n5egNdX-W9a) [videos](https://www.youtube.com/watch?v=NVAXjTzqTyE), including the [Godot documentation](https://docs.godotengine.org/en/stable/) to help me with my progress, I've completed my 2D action-adventure game prototype with fun combat mechanics, responsive enemy AI, and a rewarding character progression system.

* "What if the monsters were afraid of you?" This simple question became the foundation for my 2D RPG project developed in Godot. The journey from concept to playable prototype has been educational, teaching me about the importance of game architecture, the importance of clean code organization, and the way in which subtle design choices influence player experience. Through a repetitive process of testing and iteration, I've created a system that combines responsive, tight controls with simple combat depth. The player controller itself went through many iterations before landing on its present state-based methodology, which now incorporates directional attacks (side, front, back) and smooth animation transitions. Another of my greatest breakthroughs was appropriately separating the movement logic from the animation control, which rendered the code not only easier to maintain but also enabled combat responses and character feedback to be smoother.

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

* Although I wasn't able to present at the Expo, preparing materials for my Godot RPG game provided solid development experience. Writing an [elevator pitch](https://docs.google.com/document/d/1eUcpb7xYFhte2HqKPQu0VUC9tk6FABAEW6d1Kk7Ocwk/edit?tab=t.0) helped me to create my "monsters fear you" concept - a 2D action game with dynamic AI where enemies react the distance of the player. Creating [presentation slides](https://docs.google.com/presentation/d/1cFYzm5opI5ny_-1chUQ16AM9azGcj70A4w5eEcBYd08/edit?slide=id.p#slide=id.p) revealed technical flaws in my collision systems that needed to be debugged, namely the Y-sorting and Area2D hitboxes shown in my figures. Writing my work up for presentation helped to elucidate Godot's node structure since I had to clearly describe systems like directional combat and knockback physics. While not shared openly, going through these materials eventually made me a better considered developer, since I had to think about both the efficiency of code and how one effectively conveys technical decisions - qualities which are present in my project's README documentation and commit history

* For this blog entry, I am currently in the "Communicating the Results" step of the Engineering Design Process (EDP), where I’m documenting the technical and creative choices that shaped my game’s development. While finalizing this project, I’ve been focusing on the "Attention to Detail" skill. It’s an important skill for me because it helps me make sure that my code is clean, my animations are seamless, and every gameplay interaction works as intended. It helps me catch bugs and polish rough edges, turning a functional prototype into a professional-quality game. Another important skill I’ve practiced is "Creativity". It is an important skill to learn because it pushes me to think outside conventional solutions, whether designing dynamic knockback effects or optimizing AI behavior. These skills don’t just improve the game; they help me grow as a developer who can solve problems in ways players will remember.

[Previous](entry05.md) | [Next](entry07.md)

[Home](../README.md)