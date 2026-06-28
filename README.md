# 🤖 Universal Mathematical Foundations of Autonomous Robotics

> 🧠 **Core Insight**
>
> There is **no single universal robot model**, but nearly all autonomous systems
> share a **common mathematical backbone based on geometry, dynamics, control, and optimization**.

---

# 🌐 1. Configuration & State Geometry

| Concept | Canonical Form | Validity |
|--------|---------------|----------|
| Configuration Space | $q \in \mathcal{Q}$ | $\mathcal{Q}$ is a smooth manifold |
| State Space | $x = \begin{bmatrix} q \\ \dot{q} \end{bmatrix}$ | $x \in \mathbb{R}^{2n}$ |
| Degrees of Freedom | $n = \dim(\mathcal{Q})$ | Independent coordinates exist |

### 📌 Key Idea
A robot is modeled as motion on a **differentiable manifold**:
\[
\mathcal{Q} \subseteq \mathbb{R}^n \quad \text{or a Lie group (e.g., } SE(3)\text{)}
\]

---

# ⚙️ 2. Kinematics

| Tool | Equation | Condition |
|------|----------|----------|
| Forward Kinematics | $x = f(q)$ | $f$ differentiable |
| Velocity Kinematics | $\dot{x} = J(q)\dot{q}$ | Jacobian exists |
| Jacobian | $J(q) = \frac{\partial f}{\partial q}$ | Full rank (task-dependent) |

### 📌 Differential Structure
\[
\delta x = J(q)\,\delta q
\]

Singularities occur when:
\[
\det(JJ^T) = 0
\]

---

# 🧲 3. Dynamics (Core Robotics Model)

## 🔷 Newton–Euler Form
\[
M(q)\ddot{q} + C(q,\dot{q})\dot{q} + g(q) = \tau
\]

| Term | Meaning |
|------|--------|
| $M(q)$ | Mass / inertia matrix |
| $C(q,\dot{q})$ | Coriolis & centrifugal |
| $g(q)$ | Gravity vector |
| $\tau$ | Generalized input forces |

---

## 🔷 Lagrangian Formulation

\[
L(q,\dot{q}) = T(q,\dot{q}) - V(q)
\]

\[
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right)
- \frac{\partial L}{\partial q}
= \tau
\]

### Conditions
- $T, V$ continuously differentiable
- Holonomic constraints (if present)

---

## 🔷 Hamiltonian Form

\[
p = \frac{\partial L}{\partial \dot{q}}, \quad
H(q,p) = T + V
\]

\[
\dot{q} = \frac{\partial H}{\partial p}, \quad
\dot{p} = -\frac{\partial H}{\partial q} + \tau
\]

---

# 🟢 4. Positive Definite Structure (Energy Backbone)

| Matrix | Condition |
|--------|----------|
| Mass Matrix | $M(q) \succ 0$ |
| Inertia Tensor | $I \succ 0$ |
| Stiffness | $K \succ 0$ |
| Lyapunov Matrix | $P \succ 0$ |
| Covariance | $\Sigma \succ 0$ |

### 📌 Energy Property
\[
T(q,\dot{q}) = \frac{1}{2}\dot{q}^T M(q)\dot{q} > 0
\]

---

# 🎮 5. Control Laws

## 🔷 Error Definition
\[
e = q - q_d
\]

---

## 📌 Classical Controllers

### 🟦 P Control
\[
\tau = -K_P e
\]

### 🟩 PD Control
\[
\tau = -K_P e - K_D \dot{e}
\]

### 🟨 PID Control
\[
\tau = -K_P e - K_D \dot{e} - K_I \int e\,dt
\]

---

## 🚀 Advanced Robotics Control

### 🧠 Computed Torque
\[
\tau = M(q)v + C(q,\dot{q})\dot{q} + g(q)
\]

with:
\[
v = \ddot{q}_d - K_D\dot{e} - K_P e
\]

---

### 📈 LQR Control
\[
u = -Kx
\]

Riccati equation:
\[
A^T P + PA - PBR^{-1}B^T P + Q = 0
\]

---

### 🔮 MPC Control
\[
\min_{u_{0:T}} \sum_{k=0}^{T} \left(x_k^T Q x_k + u_k^T R u_k\right)
\]

Subject to:
\[
x_{k+1} = f(x_k,u_k)
\]

---

# ⚖️ 6. Stability Theory (Lyapunov Framework)

## 📌 Lyapunov Function
\[
V(x) > 0, \quad V(0)=0
\]

## 📉 Stability Condition
\[
\dot{V}(x) \le 0
\]

## 📈 Asymptotic Stability
\[
\dot{V}(x) < 0
\]

---

## 📊 System Properties

| Property | Condition |
|----------|----------|
| Stability | $V(x)$ positive definite |
| Convergence | $\dot{V}(x)<0$ |
| Controllability | $\text{rank}(\mathcal{C}) = n$ |
| Observability | $\text{rank}(\mathcal{O}) = n$ |

---

# 📐 7. Constraints

## Holonomic Constraints
\[
\phi(q) = 0
\]

## Velocity Constraints
\[
A(q)\dot{q} = 0
\]

## Dynamics with Constraints
\[
M(q)\ddot{q} + C(q,\dot{q})\dot{q} + g(q) + A^T\lambda = \tau
\]

---

# 📈 8. Tuning Relationships

## Second-order system approximation

\[
\ddot{e} + 2\zeta\omega_n \dot{e} + \omega_n^2 e = 0
\]

| Quantity | Formula |
|----------|--------|
| Natural frequency | $\omega_n = \sqrt{\frac{K_P}{M}}$ |
| Damping ratio | $\zeta = \frac{K_D}{2\sqrt{MK_P}}$ |
| Critical damping | $K_D = 2\sqrt{MK_P}$ |

---

# 🧮 9. Fundamental Assumptions

- $M(q)$ is symmetric positive definite  
- $\det(M(q)) \neq 0$  
- All state trajectories are at least $C^1$ smooth  
- Configuration space is a differentiable manifold  
- Control inputs are dimensionally consistent  
- Constraints are consistent and non-contradictory  
- A Lyapunov function exists for stability analysis  
- Jacobians exist and are locally full rank (except singularities)

---

# 🌍 10. Robot-Specific Extensions

| Robot Type | Additional Physics |
|------------|------------------|
| 🚗 Ground Robots | Tire friction, wheel slip |
| ✈️ UAVs | Aerodynamics, lift/drag |
| 🚢 Marine Robots | Hydrodynamics, wave forces |
| 🌊 Underwater Robots | Buoyancy, added mass |
| 🦾 Manipulators | Joint coupling, torque limits |
| 🐕 Quadrupeds | Contact dynamics, gait cycles |
| 🦿 Humanoids | Balance, ZMP, whole-body control |

---

# 📖 Final Insight

All robotic systems reduce to:

\[
\boxed{
\text{Geometry} + \text{Kinematics} + \text{Dynamics} + \text{Control} + \text{Optimization}
}
\]

This structure forms the **universal mathematical language of robotics**.
