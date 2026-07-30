---
marp: true
theme: academic-course
paginate: true
header: 'Fundamentos de PBR'
footer: 'IFMS · Jogos Digitais · Texturização'
---

## O que compõe um material PBR

Um material fisicamente baseado combina alguns mapas essenciais:

- **Base Color (Albedo)** — a cor pura, sem sombra nem luz
- **Roughness** — o quão áspera ou polida é a superfície
- **Metallic** — se o material é metálico ou dielétrico
- **Normal** — detalhes de relevo sem geometria extra

<div class="tip">

Comece sempre pelo Roughness: ele define 80% da leitura do material.

</div>

---

## Fluxo de trabalho no pipeline

1. Modelar o asset no **Blender**
2. Fazer o UV unwrap com atenção ao *texel density*
3. Pintar no **3D Coat**
4. Exportar e validar no **Unity**

<div class="warning">

Não deixe o UV unwrap para o final — ele condiciona toda a texturização.

</div>
