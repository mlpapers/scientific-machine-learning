# Scientific Machine Learning

## Problems and mathematical structure

- **[Solution learning](https://arxiv.org/abs/1711.10561)** (2017). Approximates a PDE solution from equations, boundary/initial conditions and observations. The original PINN formulation fits a coordinate-to-state function; solving a new problem can require another optimization.

- **[Operator learning](https://arxiv.org/abs/2108.08481)** (2021). Learns maps between function spaces, such as coefficients to solution fields. Shared parameters across discretizations distinguish the operator formulation from a fixed-grid predictor; approximation and numerical discretization remain separate errors.

- **[Hybrid models](https://arxiv.org/abs/2001.04385)** (2020). Combines known differential equations with trainable missing terms. The supplied physics restricts what must be learned; fitting observed trajectories does not uniquely identify an unknown mechanism.

## Neural solvers and equation constraints

- **[Physics-informed neural networks](https://arxiv.org/abs/1711.10561)** (2017). Uses automatic differentiation to penalize differential-equation residuals alongside data and boundary losses. Residual penalties enforce equations approximately at sampled points; they are not exact conservation constraints.

- **[Deep Ritz](https://arxiv.org/abs/1710.00211)** (2017). Minimizes a variational energy over neural trial functions. Unlike strong-form residual fitting, it uses the problem’s variational formulation; the chosen functional and admissible boundary treatment determine the solution sought.

- **[Deep Galerkin Method](https://arxiv.org/abs/1708.07469)** (2017). Trains a neural solution on randomly sampled space–time points using PDE, initial and boundary residuals. Avoids a tensor-product mesh; reported high-dimensional examples do not imply dimension-independent accuracy for arbitrary PDEs.

- **[Deep BSDE solvers](https://arxiv.org/abs/1706.04702)** (2017). Recasts suitable parabolic PDEs as backward stochastic differential equations. Neural networks approximate solution gradients along simulated paths; terminal-condition mismatch supplies the training loss.

- **[hp-VPINNs](https://arxiv.org/abs/2003.05385)** (2020). Combines neural trial functions with local polynomial test functions and domain decomposition. Weak residuals and h/p refinement connect physics-informed training to variational numerical methods.

- **[Residual-adaptive refinement](https://arxiv.org/abs/1907.04502)** (2019). Adds collocation points where PDE residuals are large. DeepXDE uses this to focus PINN training; a small residual still needs a stability argument to imply small solution error.

## Training failures and error analysis

- **[PINN failure modes](https://arxiv.org/abs/2109.01050)** (2021). Convection, reaction and diffusion examples expose optimization failures despite sufficient network expressivity. Curriculum regularization and sequential time training improve the tested cases; adding a PDE penalty alone is insufficient.

- **[Unbalanced loss gradients](https://arxiv.org/abs/2001.04536)** (2020). Wang et al. trace training failures to stiffness and unequal backpropagated gradients across loss terms. Gradient-statistics-based balancing improves their examples; the equation and boundary losses need compatible optimization scales.

- **[PINN neural tangent kernels](https://arxiv.org/abs/2007.14527)** (2020). Infinite-width analysis reveals unequal convergence rates for residual and boundary losses. Eigenvalue-based reweighting addresses this imbalance in experiments; the limiting-kernel theory is not a finite-network convergence guarantee.

- **[PINN loss curvature](https://proceedings.mlr.press/v235/rathore24a.html)** (2024). Links differential-operator conditioning to loss curvature. Adam+L-BFGS beats either alone; Nyström-preconditioned Newton-CG improves stalled solutions in the tested PDEs. This compares PINN optimizers, not neural and classical solvers.

- **[Time-ordered PINN training](https://arxiv.org/abs/2203.07404)** (2022). Weights later-time residuals according to earlier-time errors. This respects the order of an initial-value problem and improves chaotic-system benchmarks; “causal” here refers to temporal evolution, not causal discovery.

- **[Residual-to-solution error bounds](https://arxiv.org/abs/2203.09346)** (2022). De Ryck et al. bound Navier–Stokes PINN errors using training error, network size and quadrature. Regularity and PDE-specific stability enter the result; approximation capacity alone does not guarantee successful optimization.

## Learning operators and numerical updates

- **[DeepONet](https://arxiv.org/abs/1910.03193)** (2019). A branch network encodes input-function samples; a trunk network encodes output locations. Their combination predicts an output function. The operator approximation theorem does not bound optimization or generalization error.

- **[Fourier Neural Operator](https://arxiv.org/abs/2010.08895)** (2020). Learns integral kernels through Fourier-mode transformations. Demonstrates resolution transfer on Burgers, Darcy and Navier–Stokes tasks; shared weights across grids do not guarantee accuracy on unseen physical regimes.

- **[Physics-Informed Neural Operator](https://arxiv.org/abs/2111.03794)** (2021). Combines operator training on coarse data with PDE constraints evaluated at finer resolution. Connects FNO-style amortized prediction with equation-based refinement; separate pretraining cost from per-instance inference.

- **[Learned discretizations](https://arxiv.org/abs/1808.04930)** (2018). Learns spatial-derivative approximations inside a numerical time integrator. Bar-Sinai et al. obtain accurate coarse-grid dynamics on tested 1D equations; the learned component augments a solver rather than replacing its entire structure.

- **[Reduced-order operator inference](https://dspace.mit.edu/entities/publication/6120d5d1-6aa7-4437-a451-4ab5fbdac5d9)** (2016). Fits linear or low-order polynomial dynamics by least squares on projected trajectories, without full solver operators. A reduced state basis limits the model; estimating dynamics adds information beyond compressing snapshots.

- **[Solver-in-the-loop correction](https://arxiv.org/abs/2007.00016)** (2020). Backpropagates through solver rollouts to train state corrections. Earlier corrections change later inputs, unlike fixed-trajectory training. Gains depend on dynamics: the forced-Burgers experiment shows only a small advantage.

- **[MeshGraphNets](https://arxiv.org/abs/2010.03409)** (2020). Passes messages over simulation meshes to predict physical updates, with adaptive meshing in studied systems. Evaluated on cloth, solids and fluids; rollout accuracy and remeshing behavior matter beyond one-step prediction.

- **[Particle graph simulators](https://arxiv.org/abs/2002.09405)** (2020). Represents particles as graph nodes and learns interactions by message passing. Training with perturbed states reduces accumulated rollout error in the reported simulations; long-horizon performance differs from one-step fit.

- **[PDE pretraining: Poseidon](https://arxiv.org/abs/2405.19101)** (2024). Pretrains a multiscale operator transformer on fluid equations, then adapts to 15 tasks. Uses time conditioning and semigroup-based data pairing; transfer to new PDEs includes downstream training, not universal zero-shot solving.

## Dynamics, conservation and discovery

- **[Neural ODEs](https://arxiv.org/abs/1806.07366)** (2018). Parameterizes a continuous-time vector field and integrates it with an ODE solver. The solver, tolerances and gradient calculation become part of the learned system; a neural vector field need not preserve physical invariants.

- **[Latent ODEs](https://arxiv.org/abs/1907.03907)** (2019). Uses continuous latent dynamics and an ODE-RNN inference network for irregular observations. Can model observation times with a Poisson process; irregular sampling support does not itself identify the underlying physical state.

- **[Hamiltonian neural networks](https://arxiv.org/abs/1906.01563)** (2019). Learns a scalar Hamiltonian and derives dynamics through canonical derivatives. Conservation follows for the learned continuous system; numerical integration can still introduce energy drift.

- **[Lagrangian neural networks](https://arxiv.org/abs/2003.04630)** (2020). Learns a Lagrangian and obtains dynamics from Euler–Lagrange equations. Uses positions and velocities without requiring canonical momenta; the learned dynamics and numerical solver still need validation.

- **[SINDy](https://arxiv.org/abs/1509.03580)** (2015). Selects a sparse set of candidate functions to explain observed state derivatives. Compact equations depend on the chosen variables, function library, derivative estimates and excitation in the observed trajectories.

- **[PDE-FIND](https://arxiv.org/abs/1609.06401)** (2016). Extends sparse equation discovery to spatial derivatives and nonlinear terms. Multiple initial conditions can distinguish equations that explain the same single trajectory; low regression error alone need not identify a unique PDE.

## Inverse problems and uncertainty

- **[Bayesian PINNs](https://arxiv.org/abs/2003.06097)** (2020). Combines equation constraints and noisy observations in Bayesian inference. HMC gives better uncertainty estimates than tested variational/dropout alternatives in the paper; calibration remains specific to likelihood, prior and model adequacy.

- **[Simulation-based inference](https://arxiv.org/abs/1911.01429)** (2019). Uses simulations when likelihood evaluation is unavailable, including learned likelihoods, likelihood ratios and posteriors. Inference concerns parameters under a simulator; posterior confidence does not validate the simulator itself.

## Comparative evidence

- **[PINNs versus finite elements](https://arxiv.org/abs/2302.04107)** (2023). FEM was generally faster at equal or better accuracy in the tested PDEs; 1D Schrödinger results were inconclusive. Faster PINN point evaluation appeared only for 3D Poisson, after training.

- **[Mass-balance audit](https://arxiv.org/abs/2305.13920)** (2023). In two steady-state 1D groundwater cases, PINNs selected from 10,800 configurations each fit hydraulic heads well but retain larger mass-balance errors than finite volumes. Accurate fields did not ensure local or global conservation.

- **[PDEBench](https://arxiv.org/abs/2210.07182)** (2022). Compares forward and inverse PDE tasks with FNO, U-Net and PINN baselines. Metrics include boundary, conservation and frequency-dependent errors; a single aggregate field error can conceal physically relevant failures.

- **[The Well](https://arxiv.org/abs/2412.00568)** (2024). Provides 16 diverse simulation datasets with common interfaces. Baselines expose differences across physical systems; evaluate rollouts and dataset-specific dynamics rather than treating performance on one fluid equation as general simulation ability.

## Software

- **[DeepXDE](https://deepxde.readthedocs.io/en/latest/)** (documentation). Implements PINNs, operator networks and adaptive sampling for differential equations. Supports forward and inverse problems; equation residuals, boundary conditions and sampling rules remain user-specified.

## Related topics

[Geometric deep learning](https://github.com/mlpapers/geometric-deep-learning) · [Symbolic regression](https://github.com/mlpapers/symbolic-regression) · [Model predictive control](https://github.com/mlpapers/model-predictive-control) · [Bayesian inference](https://github.com/mlpapers/bayesian-inference) · [Neural nets](https://github.com/mlpapers/neural-nets) · [Evaluation](https://github.com/mlpapers/evaluation)
