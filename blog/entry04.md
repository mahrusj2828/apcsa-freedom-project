# Entry 4
##### 3/16/25

* I am still experimenting with [Godot](https://godotengine.org), a free open-source game engine that allows you to develop your own 2D & 3D or even cross-platform games using C++, C# or GDScript. With Godot, I want to make a 2D RPG based game where you could build you own character and I have been using GDScript to code and make the game. After another month of experimenting and making prototypes, I have aadditional features to my game in terms of character attributes. I have already added attributes where the character you are able to control could move and attack enemies in the game. The next step for me was to create a health and stamina bar for the main character. I reserched how to add such systems and found [many](https://www.youtube.com/watch?v=UEJcUnq2dfU) [useful](https://forum.godotengine.org/t/how-do-you-code-health-bars/26073/2) [resources](https://www.youtube.com/watch?v=aHBFlO8ZkkY) [online](https://www.youtube.com/watch?v=GQGX6h7SgSc) to help me implement them. First, I started with making the health bar first. In order to make a health bar, I needed to use the `TextureProgress` node as the root and then use `max_health` and `current_health` to set the current health. The `TextureProgress` properties are set up in the inspector where a `Texture` for the health bar background and `TextureProgress` for the fill texture are assigned, the Fill Mode is set to `Horizontal`, and the Min Value is set to 0 and Max Value to 100.

``` GDScript
    extends TextureProgress

    # Health variables
    var max_health: int = 100
    var current_health: int = 100

    func _ready():
        # Initialize the health bar
        max_value = max_health
        value = current_health
```

* Then, I figured out a way so that when the character is attacked by an enemy, their health goes down. I haven't figured out how to make it so that the character's health goes down depending on how much damage it takes yet. However, after I designed and created a functional health bar, I worked on making a stamina bar for the character so that when the character makes an attack, their stamina goes down, as well as for when they run and their stamina goes down quicker. Creating a stamina bar was relatively similar to making. health bar. I needed to use the `TextureProgress` node as the root. Then I made different variables depending on if I am running or attacking.

``` GDScript
    @export var stamina_bar: TextureProgress
    var is_running: bool = false
    var run_stamina_cost: float = 20.0  # Stamina cost per second while running
    var attack_stamina_cost: int = 30   # Stamina cost per attack
```

* I used the `.use_stamina` function, which updates the `current_stamina` variable and ensures the stamina bar UI reflects the changes based on the `run_stamina_cost` and `attack_stamina_cost` variables.

``` GDScript
    func _process(delta: float):
        if is_running:
            stamina_bar.use_stamina(run_stamina_cost * delta)

    func start_running():
        if stamina_bar.current_stamina > 0:
            is_running = true

    func stop_running():
        is_running = false

    func attack():
        if stamina_bar.current_stamina >= attack_stamina_cost:
            stamina_bar.use_stamina(attack_stamina_cost)
```

* Then I figured that I would need to add something that keeps the character from attacking when their stamina bar is depleted.

``` GDScript
    func attack():
        if stamina_bar.current_stamina >= attack_stamina_cost:
            stamina_bar.use_stamina(attack_stamina_cost)
            # Add attack logic here
        else:
            print("Not enough stamina to attack!")
```

* I will continue to experiment and try to perfect these character attributes and see how I could change them so that the health and stamina levels change based on the amount of damage taken and amount of attacks used. I also want to try to see if I can make it so that the damaga the character can deal changes based on their movement speed.

* For this blog entry, I am still currently on the Creating a Prototype part of the Engineering Design Process (EDP) where I am using different elements that I have learned so far in Godot to make an engaging and immersive game that people would like to play. I am getting closer to the Testing and Evaluating the Prototype part of the process because most of the basic characteristics and motions are finished and want to test run the game to see if there are any errors that may occur while playing the game. While working on this blog, I have been working the Attention to Detail skill. This is an important skill for me to learn becuase as I am approaching the end of creating a game, I need to make sure that the game runs as smoothly as possible so that players are engaged in what they are playing and do not quit because of a bug. Another important skill for me to learn is Creativity because I need to ensure that the game not only functions well but also stands out in terms of originality and player experience so that it keeps players invested and eager to explore more.

[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)