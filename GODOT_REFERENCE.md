# Roadmap Técnico

Motor principal: Godot 4.7 + Orchestrator (visual scripting). GDScript é usado como apoio quando o Orchestrator não cobre o recurso.

Cada item abaixo indica, quando aplicável, o equivalente conceitual em Unreal Engine (motor anterior desta disciplina) para facilitar a atualização de material e a comparação em aula.

## Módulo 1

Engine

Editor

Assets

FileSystem Dock (equivalente a Content Browser)

Node e Scene Tree (equivalente a Actors)

Nodes especializados como filhos (equivalente a Components)

Orchestrator (equivalente a Blueprint)

CharacterBody2D / CharacterBody3D (equivalente a Character)

move_and_slide (equivalente a Character Movement)

Input Map e InputEvent (equivalente a Enhanced Input)

Terrain3D — addon (equivalente a Landscape, sem equivalente nativo)

SDFGI / VoxelGI (equivalente a Lumen)

Sem equivalente direto a Nanite — Godot não possui geometria virtualizada; discutir como ponto de comparação (LOD manual, imposters, occlusion culling)

Exportação de projeto (equivalente a Packaging)

---

## Módulo 2

Gameplay Framework

Autoload / Singleton (equivalente a GameMode e GameState — Godot não separa os dois nativamente)

Player node + lógica de input no próprio Character (equivalente a PlayerController — Godot não tem separação nativa Pawn/Controller)

Autoload persistente entre cenas (equivalente a GameInstance)

Interfaces via GDScript (class_name + has_method / duck typing) ou nós de interface do Orchestrator (equivalente a Blueprint Interfaces)

Signals (equivalente a Event Dispatchers)

Composição de Nodes filhos (equivalente a Actor Components)

Resource customizado — .tres (equivalente a Data Assets)

Resource em coleção, Dictionary ou importação de CSV (equivalente a Data Tables)

Structs → Godot não tem struct nativo; usar Resource simples ou Dictionary tipado

Enums (nativo em GDScript e no Orchestrator)

---

## Módulo 3

AnimationTree + StateMachine (equivalente a Animation Blueprint)

BlendSpace1D / BlendSpace2D (equivalente a Blend Spaces)

AnimationPlayer / tracks de animação (equivalente a Montages)

Control nodes (equivalente a UMG)

CanvasLayer + Control (equivalente a HUD)

NavigationServer / NavigationRegion (equivalente a Navigation)

LimboAI ou Beehave — addons (equivalente a Behavior Trees, sem equivalente nativo)

Blackboard do addon de Behavior Tree escolhido (equivalente a Blackboards)

Inventory (sistema próprio baseado em Resource)

Interaction (Area3D / RayCast3D)

---

## Módulo 4

Materials (StandardMaterial3D / ShaderMaterial)

Material Overrides / Unique Materials (equivalente a Material Instances)

MultiMeshInstance3D (equivalente a Foliage)

Otimização (instancing, LOD, occlusion culling)

Profiler / Debugger nativo do Godot (equivalente a Profiling)

Exportação de projeto / Export Templates (equivalente a Packaging)

Build

---

## Módulo 5

Godot Demo Projects (oficiais)

TPS Demo (Third Person Shooter, oficial)

Platformer 2D Demo (oficial)

Projetos da Godot Asset Library

Unity

Unreal Engine

O3DE

Stride

CryEngine

Comparação arquitetural

---

## Fora do Escopo

GDExtension em C++ avançado

Networking / Multiplayer de alta escala

Dedicated Server

Engine Source (código-fonte do Godot)

Shaders avançados (além do necessário para Materials)

Rendering pipeline customizado

Editor Plugins avançados (além do uso do Orchestrator)
