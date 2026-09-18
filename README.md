# AstroScrap — Technical Design Document \& Prototype



![Unreal Engine 5.8](https://img.shields.io/badge/Unreal%20Engine-5.8-orange?logo=unrealengine)

![Physics](https://img.shields.io/badge/Physics-Newtonian%20Zero--G-blue)

![License](https://img.shields.io/badge/License-MIT-green)



A scalable, physics-based Zero-G sandbox survival game developed in Unreal Engine 5. Players navigate asteroid fields using Newtonian orbital mechanics, extract resources, and manipulate debris using a modular interaction system.



---



## Key Features



- **Newtonian Gravity Zone:** Celestial bodies exert radial gravitational acceleration calculated in real time using $F = \\frac{G \\cdot M\_1 \\cdot M\_2}{d^2}$.

- **Zero-G Inertial Movement:** Custom character mobility built on `CharacterMovementComponent` in `Flying` mode (Gravity Scale = 0) with configurable deceleration.

- **Modular Interaction Interface (`BPI\_Interactable`):** Interface-driven Grab, Hold, and Throw mechanics avoiding tight class coupling.

- **Charged Throw \& Dynamic HUD Gauge:** Variable impulse power system tied to an arc-filling radial UI gauge.

- **Real-Time Telemetry \& Visual Debug:** In-game telemetry printing force vectors, targeting line-traces, and gravity zone entry/exit logs.



---



## System Architecture

[ Astéroïde / GravityZone ]

│  (Calcul Newtonian: G \* M1 \* M2 / d²)

▼

┌───────────────┬───────────────────────────────┐

│               │                               │

▼               ▼                               ▼

[ Rigid Body ] \[ CharacterMovement ]  \[ Modular Interface ]

(Add Force)    (Add Force - Flying)   (BPI\_Interactable)



---



## Technical Specifications \& Settings



| Parameter | Value / Mode | Notes |

| :--- | :--- | :--- |

| **Movement Mode** | `Flying` | Prevents standard walking floor checks and friction |

| **Gravity Scale** | `0.0` | Bypasses UE5 global downward gravity |

| **Gravitational Scale ($G$)** | `980.0` | Gameplay-aligned scale factor (cm/s²) |

| **Max Force Clamp** | `100,000.0` | Prevents infinity division when distance $d \\to 0$ |

| **Braking Deceleration** | `0.0` | Pure zero-friction inertia (compensated by Jetpack) |

| **Interaction System** | `BPI\_Interactable` | Interface-based detection via `LineTraceByChannel` |



---



## Project Setup \& Installation



### Prerequisites

- Unreal Engine 5.8 or higher

- Git LFS (Large File Storage enabled)



### Clones \& Execution

1. Clone the repository: ```bash git clone [https://github.com/YourUsername/AstroScrap.git](https://github.com/YourUsername/AstroScrap.git)



1. Open AstroScrap.uproject in Unreal Engine 5.8.
2. Build C++ source files if prompted.
3. Press Play in the main level (Content/Maps/Main\_Sandbox).


---


## Controls


Action Control (Keyboard / Mouse)
Move / Pitch / Yaw W, A, S, D / Mouse Movement
Ascend / Descend Space / C (Flying Mode)
Interact / Grab Object E
Charge ThrowHold Left Mouse Button
Release / ThrowRelease Left Mouse Button


---


## Development Roadmap


[x] Newtonian gravity calculation \& stability optimization

[x] Zero-G player movement configuration (Flying mode)

[x] Interface-driven BPI\_Interactable Grab \& Throw system

[x] Radial HUD charging gauge \& diagnostic telemetry

[ ] Manual BPC\_Jetpack component for directional thrust

[ ] Survival indicators (Oxygen $O\_2$, Power, Health)

[ ] Chaos Physics integration for destructible asteroids

[ ] Modular station building \& scrap recycling


---


## License

Distributed under the MIT License. See LICENSE for more information.

