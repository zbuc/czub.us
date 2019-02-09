+++
title = "First Steps"
description = "The first steps towards making a game and learning Rust: design and background"
date=2019-02-09

[extra]
author = "Chris Czub"
+++

# First Steps

The first thing I should probably do is identify what kind of game to make.

My thought is that a **Tower Defense**-style game should be relatively easy to develop and fun to play. Once the very basic mechanics are down, it provides a good basis for expansion as well: there are a lot of interesting mechanics that can be added to a Tower Defense-style game to differentiate it.

## Tower Defense?

Tower Defense is a genre of game I'm first aware of appearing around the time of Starcraft 1, in the late 90s. I remember it being one of the most popular "[Use Map Settings](https://starcraft.fandom.com/wiki/UMS)"-style custom maps for the game, where they had a pretty cool map editor with scripting capabilities that allowed developers to extend the game beyond being just an RTS.

![Starcraft Tower Defense](/images/starcraft_tower_defense.jpg)
<div class="subtitle">This is what a typical Tower Defense map in Starcraft 1 looked like -- not pretty</div>

The basic rules of the game are simple. The player starts with a score set at a fixed value -- if this score falls to 0, the game is over and they lose. Enemies spawn in **waves** that get progressively more difficult as the game progresses. The enemies appear from one or more source locations and try to run to goal locations. The wave does not end until every enemy of the wave has been removed from the map; either by killing them or by them reaching the goal, where they'll be removed and points deducted from the player's score for failing to stop them. 

There is a map with some immovable physical features that provide boundaries, there is an area of the map that is considered the "goal", and there is a path from the **enemy spawn** to the **enemy goal**. The player typically might have an avatar that can run around and build **towers** that will fire at the enemies and cause them damage. The goal for the player is to stop as many enemies as possible.

After the wave ends, there is typically a short cool-down/building period where the player receives money based on their performance, the player can build additional towers or upgrade existing ones, and then get in place for the next round.

The genre remains popular today, with versions existing in Warcraft 3, Starcraft II, and even popular standalone games like [Fieldrunners](http://subatomicstudios.com/games/fieldrunners/).

![Fieldrunners](/images/fieldrunners.jpg)
<div class="subtitle"><strong>Fieldrunners</strong> is a popular standalone mobile/PC Tower Defense game</div>

I doubt I'll ever reach the polish of a commercial game like Fieldrunners, but I'd like to at least make something fun to play.

## My Initial Game Features

The initial feature list for my proof-of-concept game is this:

- Display a **game map**
- The player can place **towers** on the map
- The player has a **budget** that can't be exceeded and is replenished after every wave
- Enemies come in **waves** and proceed from their **spawn** to their **goal**
- There is a **victory condition** for the game (a certain number of waves completed, based on the map)
- Towers fire at enemies
- The player's score starts at a certain value, based on the map
- When enemies reach the enemy goal zone, they deduct from the player's score
- There is a loss condition for the game when the player's score reaches zero

## Learning Rust

I need to learn Rust to do this. Last night, I started my process of learning Rust by starting to read [the book](https://doc.rust-lang.org/book). I got to the end of chapter 6 before falling asleep. The second chapter of the book has you write a basic "guess the number" game to learn how a Rust program works, and then you start learning the other features of the language. By the end of chapter 6, I knew enough to start writing the basic data structs I thought I _might_ need for my game, but not much else.

```rust
use std::io;
use std::cmp::Ordering;
use rand::Rng;

mod geometry {
    #[derive(Debug)]
    pub struct Point(pub u32, pub u32);

    #[derive(Debug)]
    pub struct BoundingBox(pub Point, pub Point);

    impl BoundingBox {
        pub fn area(&self) -> u32 {
            ((self.1).0 - (self.0).0) * ((self.1).1 - (self.0).1)
        }
    }
}

mod game {
    use crate::geometry;

    #[derive(Debug)]
    pub struct GameMap {
        pub name: String,
        pub dimensions: geometry::BoundingBox,
    }

    #[derive(Debug)]
    pub enum GameEntityType {
        Player,
        Enemy,
        Structure,
        Zone,
        Projectile,
    }

    #[derive(Debug)]
    pub struct GameEntity {
        pub location: geometry::Point,
        pub entity_type: GameEntityType,
    }

    impl GameEntity {
        fn can_take_damage(&self) -> bool {
            match self.entity_type {
                GameEntityType::Player => true,
                GameEntityType::Enemy => true,
                GameEntityType::Structure => true,
                GameEntityType::Zone => false,
                GameEntityType::Projectile => false,
            }
        }
    }

    #[derive(Debug)]
    enum GameMessage {
        Interact{source: GameEntity, target: GameEntity},
        TriggerAbility{target: GameEntity},
        Move{target: GameEntity, destination: geometry::Point},
    }

    #[derive(Debug)]
    pub struct GameState {
    //    entities: 
    }

    #[derive(Debug)]
    pub struct ActiveGame {
        pub map: GameMap,
        pub state: GameState,
        pub started_time: u32,
    }

    pub fn get_default_map() -> GameMap {
        GameMap {
            name: String::from("Test"),
            dimensions: geometry::BoundingBox (
                geometry::Point(0,0),
                geometry::Point(100,100)
            )
        }
    }

    pub fn start_game(map: GameMap) -> ActiveGame {
        ActiveGame {
            map: map,
            state: GameState {
                
            },
            started_time: 0,
        }
    }
}

fn main() {
    let map = game::get_default_map();
    let game = game::start_game(map);

    println!("Game started: {:#?}", game);

    println!("Game bbox area: {}", game.map.dimensions.area());
}
```
<div class="subtitle">The very first Rust code I wrote last night</div>

I did a little research into game development in Rust, to see what other people were doing. There seem to be a handful of popular game engine libraries: [Amethyst](https://github.com/amethyst/amethyst), [ggez](https://github.com/ggez/ggez), and [Piston](https://github.com/PistonDevelopers/piston) looked most promising to me, and there were also the excellent resources at [Are we game yet?](http://arewegameyet.com/).

I considered using one of these pre-packaged engines, but figured that I don't really need to: my game is pretty simple, and the point is to learn anyways. But this doesn't mean I'm going to build my own engine, per se. An engine is a set of reusable components that can be used to build any game; my components might only be useful for my game. But that's fine.

Ian Mallett's blog has a mirror of an [excellent post](https://geometrian.com/programming/tutorials/write-games-not-engines/) by "scientificninja" about writing game engines vs. games, and I let this principle guide me:

> So my advice to you, if you’re trying to write an engine, is: don’t. No matter what your reasons are—it doesn’t matter if you’re writing an engine so you can write your dream game, or if you’re writing an engine because you think it will be a good learning experience, or any number of similar reasons—they’re all wastes of time. You can sit down and write a game without first writing an engine, and in fact this is very often the better approach, regardless of why you want to write an engine. The entire development process goes much more smoothly if you are focused on writing a game instead: a game is much easier to identify requirements for, much narrower in focus, much more rewarding when finished, and much, much more useful.
>
> The solution, even if you really want to make an engine, is to make a game instead. I can hear you crying out in protest from here, but just bear with me for a minute. The game does not have to be an epic production. It does not have to be GTA5, Quake 17, the next Elder Scrolls game, or a WoW-killer. It just has to be a game, with well defined (and ideally well thought out) gameplay and well defined developmental scope. A game is much easier to identify requirements for, as I’ve already mentioned, and it is also a practical application of those requirements. Once you have made one game, make another. Then another. Each time you start a new project, you should identify functionality that could be used and pull it out into a common library of base code. You’ll probably have to refactor some of your code to remove explicit dependencies on other code or data that is game specific, but this is a good thing. It will help you generalize what is generalizable in a way that you can still test the generalized functionality against your finished game and confirm that it still works (obviously you might have to modify some game-specific code to adapt to the increased generality, as well).
<div class="subtitle"><strong>-- scientificninja</strong></div>

## Library Selection

I did a bit of exploration of the libraries available to me, and think I've selected at least some to evaluate for my initial pass at the game.

For 3D graphics, I will try to use [gfx-rs](https://github.com/gfx-rs/gfx), a cross-platform, backend-agnostic graphics abstraction layer that supports OpenGL, DirectX, Vulkan, and Metal for 3D graphics.

For windowing, I am looking at [winit](https://github.com/tomaka/winit). I saw [this blog post](https://suhr.github.io/gsgt/) that went over using a library called [glutin](https://github.com/tomaka/glutin), but this looked to only support OpenGL and **winit** seemed to provide the same sort of functionality, but in a more agnostic manner. Regardless, the post was very helpful for providing some basic glimpse into how Rust code interfacing with **gfx-rs** might look.

## Zzz...

And that brings us to the end of day 1. I have a good idea of the game I'm going to make, I have some libraries to look into, and I made some progress in learning the language.

Oh, I also set up this blog this morning, so I would have somewhere to document this and other projects. I haven't blogged in so long. Since I was learning Rust, I decided to use a Rust-based static site generator called [Zola](https://github.com/getzola/zola) and modified a template called [Dinkleberg](https://github.com/rust-br/dinkleberg) to suit my tastes.