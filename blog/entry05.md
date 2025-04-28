# Entry 5
##### 04/27/25

* I am still experimenting with [Godot](https://godotengine.org), a free open-source game engine that allows you to develop your own 2D & 3D or even cross-platform games using C++, C# or GDScript. Over the past month, I've made significant progress in developing more sophisticated game systems that bring my vision closer to reality. While my prototype already had functional character movement and basic combat, I knew the game needed deeper RPG mechanics to create meaningful player progression and customization. After studying several successful indie RPGs and reviewing [Godot documentation](https://docs.godotengine.org/en/stable/) on state management, I designed an attribute system that would serve as the foundation for all character development. The system needed to be flexible enough to support different character builds while remaining easy to balance. I wanted attributes to affect not just combat numbers, but also movement, special abilities, and even dialogue options in some cases. After several iterations, I settled on a resource-based approach that separates the raw stat data from the character nodes themselves. This makes it easier to create preset builds for NPCs while allowing player stats to evolve throughout the game. Here's the core implementation:

``` gdscript
class_name CharacterStats
extends Resource

@export_category("Core Attributes")
@export var strength: int = 5 : set = set_strength
@export var agility: int = 5 : set = set_agility
@export var vitality: int = 5 : set = set_vitality
@export var intelligence: int = 5 : set = set_intelligence

@export_category("Derived Stats")
@export var max_health: int = 50
@export var physical_damage: float = 7.0
@export var attack_speed: float = 1.0

func set_strength(value: int) -> void:
    strength = value
    recalculate_stats()

func set_agility(value: int) -> void:
    agility = value
    recalculate_stats()

func recalculate_stats() -> void:
    max_health = vitality * 10 + strength * 2
    physical_damage = strength * 1.2 + agility * 0.5
    attack_speed = 1.0 + (agility * 0.02)
    stats_updated.emit()
```

* The real breakthrough came when I connected this to a signal-based UI system that updates all relevant displays whenever stats change. Now when players allocate points during level-up or equip new gear, they immediately see the impact on their character's capabilities. I've already prototyped several talent trees that will modify these base formulas in interesting ways, like allowing strength to boost magic damage for battlemages or making agility improve critical hit chance for rogues. The resource-based design makes it easy to save and load different builds, which will be perfect for the New Game+ mode I'm planning.

* One of my biggest breakthroughs this month was implementing a dynamic dialogue system that reacts to character stats and quest progress. Instead of generic NPC responses, characters now comment on your strength level or completed quests:

``` gdscript
func get_dialogue():
    if PlayerStats.strength > 20:
        return "Whoa, you're jacked! The arena's down the street."
    elif QuestSystem.has_quest("Missing Heirloom"):
        return "Any luck finding my grandmother's necklace?"
    else:
        return default_dialogue
```

* The system uses Godot's `DialogueManager` plugin with custom conditions that check various game states. I've added special interactions when wielding certain weapons too:

``` gscript
func _on_npc_interact():
    if Equipment.current_weapon == "Royal Sword":
        show_dialogue("That blade... are you from the capital?")
    else:
        show_dialogue(default_greeting)
```

* I also added a day/night cycle, where nstead of a simple timer, it now affects NPC schedules, enemy spawns, and shop hours:

``` gdscript
func _on_hour_changed(hour):
    if hour == 22: # 10PM
        close_shops()
        spawn_night_creatures()
        update_lighting(0.3) # Dim the world

    elif hour == 6: # 6AM
        open_shops()
        despawn_night_creatures()
        update_lighting(1.0)
```

* I also implementedin code when taking damage:

``` gdscript
func take_damage(amount):
    health -= amount
    $Sprite.material.set_shader_parameter("hit_intensity", 0.8)
    await get_tree().create_timer(0.2).timeout
    $Sprite.material.set_shader_parameter("hit_intensity", 0)
```

* For this blog entry, I am currently in the "Testing and evaluating the prototype" and "Improve as needed" steps of the Engineering Design Process (EDP) where I am testing out the code that I have already implemented and improving on sections that might not be runnning smoothly to enhance the player's experience when playing my game. While working on this blog, I have been working on the "Growth Mindset" skill. It is an important skill for me to learn because it keeps me resilient when facing bugs and design challenges, allowing me to view failures as learning opportunities rather than obstacles. This mentality helps me persistently refine systems like combat and AI, turning setbacks into stepping stones toward a better game. Another important skill for me to learn is the "Consideration" skill because it ensures my game remains engaging and accessible for players, not just functional for me, creating experiences that feel polished and rewarding rather than frustrating or inconsistent.

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)