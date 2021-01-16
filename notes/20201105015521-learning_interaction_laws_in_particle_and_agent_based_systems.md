---
title: Learning interaction laws in particle and agent based systems
---

# Tags
[phd](20201105015702-phd.md) [machine-learning](20201105015715-machine_learning.md) [collective-dynamics](20201105015744-collective_dynamics.md) [cooperation-dynamics](20201105015758-cooperation_dynamics.md) [dynamical-systems](20201104234038-dynamical_systems.md)


# Popular model for agent-based systems

Observations: \\(\\{(\mathbf{x}\_i, \dot{\mathbf{x\_i}})^{(m)} (t\_\ell) \\}\_{i=1...N,\ell=1...L,m=1...M}\\),
Where \\(\mathbf{x}^{(m)} \sim \mu\_0\\)

\\(N\\) agents, \\(M\\) trajectories, \\(L\\) time-steps

\\[
{\dot{\mathbf{x}}\_i}^{(m)}(t) = \frac{1}{N} \sum\_{i'=1}^{N} \mathbf\phi \big( \lVert \mathbf{x}\_i}^{(m)}(t) - \mathbf{x}\_{i'}^{(m)}(t) \rVert \big)\big( \mathbf{x}\_{i'}^{(m)}(t) - \mathbf{x}\_i^{(m)}(t) \big)
\\]

Where \\(\phi\\) is the interaction kernel. Note that it is a one-dimensional function.
