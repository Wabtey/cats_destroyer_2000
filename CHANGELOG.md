# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Working demo! - 2024-08-08

[![v1.0.0](https://img.shields.io/badge/v1.0.0-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v1.0.0)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v1.0.0)

### Bevy Migration to `0.14`

### Bevy `0.14`

[Migration Guide Bevy 0.13 -> 0.14](https://bevyengine.org/learn/migration-guides/0.13-0.14/)

- Dependencies
  - bevy_rapier_2d `0.27` - [bevy_rapier changelog](https://github.com/dimforge/bevy_rapier/blob/master/CHANGELOG.md#v0270-07-july-2024) and [rapier changelog `0.18` to `0.21`](https://github.com/dimforge/rapier/blob/master/CHANGELOG.md#v0210-23-june-2024)
    - `Rapier_Configuration` doesn't derive `Default`
  - bevy-inspector-egui `0.25` - [changelog](https://github.com/jakobhellermann/bevy-inspector-egui/compare/v0.24.0...v0.25.0)
- ECS
  - Colors
    - [colors import](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#css-constants)
    - [`rgb` to `srgb`](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#color-methods)
  - [Deprecate `SpriteSheetBundle` and `AtlasImageBundle`](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#deprecate-spritesheetbundle-and-atlasimagebundle)
  - [Use `UVec2` when working with texture dimensions](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#use-uvec2-when-working-with-texture-dimensions)
  - [Schedules `Startup` runs after `OnEnter`](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#onenter-state-schedules-now-run-before-startup-schedules)
  We don't have anything to change as we have only Startup system `spawn_camera`; the camera will only be use in `Update`.
  Note that you can create `SubState` with a source.
  - [ECS observers were introduced: mechanisms for immediately responding to events in the world.](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#generalised-ecs-reactivity-with-observers)
  - [Make `apply_state_transition` private](https://bevyengine.org/learn/migration-guides/0-13-to-0-14/#make-apply-state-transition-private)

#### WGPU error

```text
ERROR wgpu_hal::gles: wgpu-hal heuristics assumed that the view dimension will be equal to `D2` rather than `D2Array`.
`D2` textures with `depth_or_array_layers == 1` are assumed to have view dimension `D2`
`D2` textures with `depth_or_array_layers > 1` are assumed to have view dimension `D2Array`
`D2` textures with `depth_or_array_layers == 6` are assumed to have view dimension `Cube`
`D2` textures with `depth_or_array_layers > 6 && depth_or_array_layers % 6 == 0` are assumed to have view dimension `CubeArray`
```

### Bevy `0.13`

[Migration Guide Bevy 0.12 -> 0.13](https://bevyengine.org/learn/migration-guides/0.12-0.13/)

- Dependencies
  - bevy_rapier_2d `0.25` - [changelog](https://github.com/dimforge/bevy_rapier/blob/master/CHANGELOG.md#v0250-19-feb-2024)
    - Collisions between the character controller and sensors are now disabled by default.
  - bevy-inspector-egui `0.24` - [changelog](https://github.com/jakobhellermann/bevy-inspector-egui/compare/v0.22.0...v0.24.0)
- ECS
  - [Ensure calls to `EventWriter::send` either handle the returned value, or suppress the result with `;`.](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#update-event-send-methods-to-return-eventid)
  - [Replace `Option<With<T>>` with `Has<T>`](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#split-worldquery-into-querydata-and-queryfilter)
  - [Rename `Input` to `ButtonInput`](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#rename-input-to-buttoninput)
  - [Texture Atlas rework](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#texture-atlas-rework)
    - `SpriteSheetBundle` now uses a `Sprite` instead of a `TextureAtlasSprite` component
    - `mut atlases: ResMut<Assets<TextureAtlas>>` to `mut atlases: ResMut<Assets<TextureAtlasLayout>>`
    - `TextureAtlas::from_grid` to `TextureAtlasLayout::from_grid`
  - [Renamed `App::add_state` to `init_state`.](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#add-insert-state-to-app)
  - [`KeyCode` rename](https://bevyengine.org/learn/migration-guides/0-12-to-0-13/#update-winit-dependency-to-0-29)
    - `KeyCode::W` -> `KeyCode::KeyW`
    - `KeyCode::Up` -> `KeyCode::ArrowUp`
    - `KeyCode::Key1` -> `KeyCode::Digit1`

### Bevy `0.12`

[Migration Guide Bevy 0.11 -> 0.12](https://bevyengine.org/learn/migration-guides/0.11-0.12/)

- Dependencies
  - bevy_rapier_2d `0.23` - [changelog](https://github.com/dimforge/bevy_rapier/blob/master/CHANGELOG.md#0230)
- ECS
  - no longer need to manually configure the `ChangeWatcher` in the `AssetPlugin` as it is now configured automatically when the feature is enabled.
  - [`EventReader::iter` to `EventReader::read`](https://bevyengine.org/learn/migration-guides/0-11-to-0-12/#refactor-eventreader-iter-to-read)
  - [`RemovedComponents::iter` to `RemovedComponents::read`](https://bevyengine.org/learn/migration-guides/0-11-to-0-12/#rename-removedcomponents-iter-iter-with-id-to-read-read-with-id)
  - [If you were using Bevy's `bevy_dylib` feature, use Bevy's `dynamic_linking` feature instead.](https://bevyengine.org/learn/migration-guides/0-11-to-0-12/#remove-the-bevy-dylib-feature)

## Back to jail - [v0.4.0](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.4.0) - 2024-08-08

[![v0.4.0](https://img.shields.io/badge/v0.4.0-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.4.0)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.4.0)
[![**Full Commits History**](https://img.shields.io/badge/GitHubLog-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/compare/v0.3.0...v0.4.0)](https://github.com/Fabinistere/cats_destroyer_2000/compare/v0.3.0...v0.4.0)

### Features

- reset the level when getting caught (bevy asset bug: the assets will wrongly unload while storng handle is alive after the level reset - fixed in `13.2`)
- the enemies can't catch you if you're in another location's room (corridor/spawn)

## Bevy Migration - [v0.3.0](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.3.0) - 2024-08-06

[![v0.3.0](https://img.shields.io/badge/v0.3.0-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.3.0)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.3.0)
[![**Full Commits History**](https://img.shields.io/badge/GitHubLog-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/fabinistere/cats_destroyer_2000/commits/v0.3.0)](https://github.com/fabinistere/cats_destroyer_2000/commits/v0.3.0)

- [Migration Guide Bevy 0.10 -> 0.11](https://bevyengine.org/learn/migration-guides/0.10-0.11/)
- *not needed* [Changelog Bevy Rapier 0.21 -> 0.22](https://github.com/dimforge/bevy_rapier/blob/master/CHANGELOG.md#0220-10-july-2023)

### Added

- [![MIT/Apache 2.0](https://img.shields.io/badge/license-MIT%2FApache-blue.svg)](https://github.com/fabinistere/cats_destroyer_2000#license)

### [Bevy 0.11](https://bevyengine.org/learn/migration-guides/0.10-0.11/) Migration

- ECS
  - `in_set(OnUpdate(*))` -> `run_if(in_state(*))`
  - Add the `#[derive(Event)]` macro for events.
  - Allow tuples and single plugins in `add_plugins`, deprecate `add_plugin`
  - [Schedule-First: the new and improved `add_systems`](https://bevyengine.org/learn/migration-guides/0.10-0.11/#schedule-first-the-new-and-improved-add-systems)
- UI
  - Flatten UI Style properties that use Size + remove Size
    - The `size`, `min_size`, `max_size`, and `gap` properties have been replaced by the `width`, `height`, `min_width`, `min_height`, `max_width`, `max_height`, `row_gap`, and `column_gap` properties. Use the new properties instead.
  - [Remove `Val::Undefinded`](https://bevyengine.org/learn/migration-guides/0.10-0.11/#remove-val-undefined)
    - `Val::Undefined` has been removed. Bevy UI’s behaviour with default values should remain the same.
    The default values of `UiRect`’s fields have been changed to `Val::Px(0.)`.
    `Style`’s position field has been removed. Its `left`, `right`, `top` and `bottom` fields have been added to `Style` directly.
    For the `size`, `margin`, `border`, and `padding` fields of `Style`, `Val::Undefined` should be replaced with `Val::Px(0.)`.
    For the `min_size`, `max_size`, `left`, `right`, `top` and `bottom` fields of `Style`, `Val::Undefined` should be replaced with `Val::Auto`
  - [Rename keys like `LAlt` to `AltLeft`](https://bevyengine.org/learn/migration-guides/0.10-0.11/#rename-keys-like-lalt-to-altleft)
  - [Delay asset hot reloading](https://bevyengine.org/learn/migration-guides/0.10-0.11/#delay-asset-hot-reloading)
  - [`Interaction::Clicked` replaced by `Interaction::Pressed`](https://bevyengine.org/learn/migration-guides/0.10-0.11/#rename-interaction-clicked-interaction-pressed)
- Dependencies
  - bevy_rapier_2d `0.22`
  - bevy-inspector-egui `0.20`

### [Bevy 0.10](https://bevyengine.org/learn/migration-guides/0.9-0.10/) Migration

- Dependencies
  - remove the `dynamic` feature fr
  - bevy-inspector-egui `0.18`
  - bevy_rapier2d `0.21` - [changelog](https://github.com/dimforge/bevy_rapier/blob/master/CHANGELOG.md#0210--07-march-2023)
    - feature `debug-render` change to `debug-render-2d`
- ECS
  - [Migrate engine to Schedule v3 (stageless)](https://bevyengine.org/learn/migration-guides/0.9-0.10/#migrate-engine-to-schedule-v3-stageless)
  - [System sets (Bevy 0.9)](https://bevyengine.org/learn/migration-guides/0.9-0.10/#system-sets-bevy-0-9)
  - [States](https://bevyengine.org/learn/migration-guides/0.9-0.10/#states)
  - Replace `RemovedComponents<T>` backing with `Events<Entity>`
- UI
  - [Windows as Entities](https://bevyengine.org/learn/migration-guides/0.9-0.10/#windows-as-entities)

## Final Cinematic - [v0.2](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.2) - 2023-06-11

[![v0.2](https://img.shields.io/badge/v0.2-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.2)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.2)

## Add

- End cinematic
- WebAssembly

## Must Have - v0.2

- Back to jail (when touched by a enemy)

## Should Have - v0.2

- UI for the Tablet
- Vision Feature
  - Tile per Tile
  - Can only interact with seen entities.
  - Entities can be seen by camera, any mindControled entity (including the player)
- Music
- SFX
- Start Menu

## Level 1000 - [v0.1](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.1) - 2023-02-12

[![v0.1](https://img.shields.io/badge/v0.1-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.1)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.1)

## Currently Have

- NPC
  - triggered by player if around (and in the same area)
  - Movement
- Player
  - Basic Movement
- Tablet
  - MindControl
    - Take the body of another cat
    - Stun after a short time after mindctrl
  - Hack
    - Open One door
    - Can't Hack while mindcontrol
- Map
  - Hitbox
  - Doors
    - Closed
  - Physical Button
    - which opens front and exit doors

## Must Have - v0.1

- Start/End cinematic
- Back to jail (when touched by a enemy)
- Web Exe

## Should Have - v0.1

- UI for the Tablet
- Vision Feature
  - Tile per Tile
  - Can only interact with seen entities.
  - Entities can be seen by camera, any mindControled entity (including the player)
- Music
- SFX
- Start Menu

## Blue Cat Flex - [v0.0](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.0) - 2023-02-03

[![v0.0](https://img.shields.io/badge/v0.0-gray?style=flat&logo=github&logoColor=181717&link=https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.0)](https://github.com/Fabinistere/cats_destroyer_2000/releases/tag/v0.0)

- Simple Animation
- Blue Cat Flexing in the center

![fast_blue_cat](https://user-images.githubusercontent.com/73140258/216720606-6e8f7768-3170-4956-a5d1-5124741783aa.gif)
