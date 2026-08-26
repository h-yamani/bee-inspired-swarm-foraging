# Experiment Guide

## Configuration families

The XML files encode controllers, actuator and sensor interfaces, role-specific probabilities, food parameters, arena geometry, robot distribution, physics engines, and visualisation settings.

| Family | Purpose |
|---|---|
| `foraging_HB*` | Honey-bee-inspired recruitment and foraging |
| `foraging_adaptive*` | Adaptive-foraging comparison |
| `foraging.xml` | Base foraging experiment |
| `diffusion*` | Obstacle-avoidance/diffusion examples |
| `flocking.xml` | Supporting flocking example |
| `synchronization.xml` | Supporting synchronisation example |
| `evolution*` | Evolution-related supporting configurations |

## Role configuration

The foraging XML files define up to three controller configurations using the historical attribute spelling `robot_typte`:

| Value | Role represented in controller logic |
|---:|---|
| `1` | Scout/search robot |
| `2` | Hive/observer robot |
| `3` | Forager/recruited robot |

The typo is preserved because changing it without changing the parser would break configuration loading.

## Common parameters

| XML area | Representative parameters |
|---|---|
| Framework | simulation length, ticks per second, random seed, threads |
| Diffusion | straight-angle range and obstacle threshold |
| Wheel turning | hard/soft/no-turn thresholds and maximum speed |
| State | resting and exploring probabilities, minimum durations, social and food rules |
| Loop functions | food items, source radius, energy per item, walking cost, output file |
| Arena | dimensions, walls, lights, nest region, robot distribution |

## Output schema

The loop-function implementation writes:

```text
# clock walking resting collected_food energy consume_energy energy_per_food
```

The exact energy accounting combines activity-state costs and reward/cost values configured or hard-coded in the legacy implementation. Interpret the fields according to the source before comparing them with modern physical energy units.

## Reproducibility caution

Several configurations set `length="0"` and `random_seed="0"`, and the repository does not include original raw outputs or an environment lockfile. A reproduction study should first define fixed seeds, finite durations, compiler/ARGoS versions, and repeated trials.

