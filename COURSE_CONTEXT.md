DISCIPLINA

Nome:
Tendências de Motores de Jogos

Carga Horária

17 semanas

2 encontros semanais

2h15 por encontro

Último semestre do curso.

OBJETIVO

A disciplina NÃO tem como objetivo ensinar Godot.

Ela utiliza Godot 4.7 + Orchestrator (visual scripting) como estudo de caso para ensinar conceitos universais presentes em Game Engines modernos.

O objetivo principal é desenvolver autonomia para que o estudante consiga aprender qualquer motor de jogos.

PERFIL DOS ESTUDANTES

Os estudantes já cursaram disciplinas de:

- Programação
- Game Design
- Unity
- Inteligência Artificial
- Computação Gráfica
- Projeto Integrador

Assuma que sabem desenvolver jogos.

Não ensinar conceitos básicos de programação.

FILOSOFIA

Ensinar conceitos.

Não ensinar botões.

Toda aula deve responder:

O que é?

Por que existe?

Quando utilizar?

Como funciona no Godot (via Orchestrator ou GDScript)?

Como funciona na Unity?

Como funciona em outros motores (Unreal, O3DE, Stride)?

ORGANIZAÇÃO

A disciplina possui cinco módulos.

Módulo 1
Fundamentos do Godot.

Módulo 2
Gameplay Framework.

Módulo 3
Sistemas do Motor.

Módulo 4
Vertical Slice.

Módulo 5
Comparação entre motores.

PROJETO

Toda a disciplina desenvolve um único projeto incremental.

Cada módulo adiciona novos sistemas.

Não utilizar mini games independentes.

COMPARAÇÕES

Sempre comparar Godot com Unity.

Quando pertinente citar Unreal Engine, O3DE, CryEngine ou Stride.

VERSÃO

Utilizar Godot 4.7 com o addon Orchestrator (visual scripting) como camada principal de scripting, com GDScript como apoio quando o Orchestrator não cobrir o recurso.

========================================================================
PROGRESSÃO PEDAGÓGICA
========================================================================

A disciplina evolui continuamente em autonomia.

Professor demonstra
↓

Professor demonstra e aluno replica
↓

Professor propõe desafios
↓

Professor atua como mentor
↓

Professor atua apenas como revisor

========================================================================
MÓDULO 1 — APRENDER A ENGINE
========================================================================

Metodologia dominante

Scaffolded Learning

Autonomia

Muito baixa.

Objetivo

Aprender o editor.

Conhecer a arquitetura do Godot.

Construção

Protótipo explorável.

Recursos

- Godot Editor
- Viewport (2D/3D)
- FileSystem Dock
- Node e Scene Tree
- Nodes especializados (equivalente a Components)
- Orchestrator (visual scripting)
- CharacterBody2D / CharacterBody3D
- Movimento via move_and_slide
- Input Map e InputEvent
- Materiais (StandardMaterial3D, ShaderMaterial)
- Terrain3D (addon, equivalente a Landscape)
- SDFGI / VoxelGI (iluminação global em tempo real, equivalente a Lumen)
- Exportação de projeto (equivalente a Packaging)

Produto

Primeiro Build executável.

========================================================================
MÓDULO 2 — CONSTRUIR GAMEPLAY
========================================================================

Metodologia dominante

Studio Based Learning

Autonomia

Baixa.

Professor demonstra conceitos.

Os estudantes adaptam.

Construção

Sistemas fundamentais.

Recursos

- Autoload / Singleton (equivalente a GameMode e GameState)
- Player node + Input handling (equivalente a PlayerController)
- Autoload persistente entre cenas (equivalente a GameInstance)
- Interfaces via GDScript (duck typing, class_name, has_method) ou nós do Orchestrator (equivalente a Blueprint Interfaces)
- Signals (equivalente a Event Dispatchers)
- Composição de Nodes filhos (equivalente a Actor Components)
- Resource customizado (equivalente a Data Assets)
- Resource em coleção / Dictionary (equivalente a Data Tables)
- FileAccess + ResourceSaver/ResourceLoader (equivalente a SaveGame)

Desafios

Portas

Baús

Alavancas

NPCs

Checkpoints

Produto

Gameplay funcional.

========================================================================
MÓDULO 3 — RESOLVER PROBLEMAS
========================================================================

Metodologia dominante

Challenge Based Learning

Autonomia

Média.

Professor apresenta problemas.

Cada grupo propõe soluções.

Recursos

- AnimationTree e AnimationTree StateMachine (equivalente a Animation Blueprint)
- BlendSpace1D / BlendSpace2D (equivalente a Blend Spaces)
- Control nodes (equivalente a UMG)
- CanvasLayer + Control (equivalente a HUD)
- Inventory (sistema próprio baseado em Resource)
- Interaction (Area3D / RayCast3D)
- NavigationAgent e NavigationServer (equivalente a AI Navigation)
- NavigationRegion (equivalente a Navigation)
- LimboAI ou Beehave (addons, equivalente a Behavior Tree)
- Blackboard (recurso do addon de Behavior Tree escolhido)

Produto

Vertical Slice jogável.

========================================================================
MÓDULO 4 — PRODUÇÃO
========================================================================

Metodologia dominante

Studio Based Learning

Autonomia

Alta.

O professor atua como diretor técnico.

Recursos

- Materials (StandardMaterial3D / ShaderMaterial)
- Material Overrides / Unique Materials (equivalente a Material Instances)
- MultiMeshInstance3D (equivalente a Foliage)
- AudioStreamPlayer (Audio)
- Otimização (instancing, LOD, occlusion culling)
- Exportação de projeto / Export Templates (equivalente a Packaging)
- Profiler / Debugger do Godot (equivalente a Profiling)

Produto

Vertical Slice final.

========================================================================
MÓDULO 5 — ENGENHARIA REVERSA
========================================================================

Metodologia dominante

Reverse Engineering

Autonomia

Muito alta.

Os estudantes analisam projetos profissionais.

Referências

Godot Demo Projects (oficiais)

TPS Demo (Third Person Shooter, oficial)

Platformer 2D Demo (oficial)

Projetos da comunidade Godot Asset Library

Discussões

Arquitetura

Boas práticas

Comparação com Unity

Comparação com Unreal Engine

Comparação com O3DE

Produto

Apresentação técnica do projeto e comparação entre motores.
