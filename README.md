<h1 align="center">Awesome Robot Learning for Bimanual Manipulation</h1>

<p align="center">
  A living collection of papers, code, datasets, benchmarks, and other resources for learning-based bimanual and dual-arm manipulation.
</p>

<p align="center">
  <a href="https://github.com/Destiny000621/awesome-bimanual-robot-learning/stargazers"><img src="https://img.shields.io/github/stars/Destiny000621/awesome-bimanual-robot-learning?style=social" alt="GitHub stars"></a>
  <a href="https://github.com/Destiny000621/awesome-bimanual-robot-learning/network/members"><img src="https://img.shields.io/github/forks/Destiny000621/awesome-bimanual-robot-learning?style=social" alt="GitHub forks"></a>
  <a href="https://github.com/Destiny000621/awesome-bimanual-robot-learning/pulls"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs welcome"></a>
  <img src="https://img.shields.io/badge/papers-70%2B-blue" alt="70+ papers">
</p>

This collection spans foundation models, LLM/VLM reasoning, vision-language-action models, world models, generative policies, imitation learning, reinforcement learning, planning, datasets, and benchmarks. It focuses on methods that explicitly study two-arm coordination or report meaningful bimanual evaluation.

> This is a curated, evolving bibliography rather than an exhaustive survey. Preprints are included and may change after peer review.

**Last updated: June 9, 2026**

## News

- **[2026-06-09]** Released the first categorized paper list with more than 70 entries.
- **[2026-06-09]** Added explicit distinctions between bimanual-specific methods, broader bimanual-evaluated methods, and related general robot-learning foundations.

## What Is Robot Learning for Bimanual Manipulation?

Robot learning for bimanual manipulation studies how a robot can acquire perception, reasoning, coordination, and control capabilities for tasks involving two arms. Beyond generating two action streams, a capable system must learn when the arms should cooperate tightly, work independently in parallel, assume asymmetric roles, hand objects over, or sequence actions around shared spatial and physical constraints.

This repository emphasizes the learning questions that distinguish modern bimanual systems:

- How are cross-arm dependencies and coordination represented?
- How do policies generalize across objects, tasks, embodiments, and environments?
- Can reusable unimanual skills be composed into efficient bimanual behavior?
- How do high-level planners coordinate low-level learned policies?
- How should demonstrations, synthetic data, simulation, and real-world experience be combined?
- How are safety, failures, uncertainty, and recovery evaluated?

## Organization

Papers are organized by their **primary system contribution**, while tags capture overlapping properties. The collection can also be read along four complementary axes:

| Axis | Examples |
|---|---|
| System role | reasoning, planning, representation, world modeling, low-level control |
| Learning paradigm | imitation learning, reinforcement learning, self-supervision, post-training |
| Policy family | VLA, diffusion, flow matching, transformer, world-model policy |
| Coordination structure | tightly coupled, asymmetric, parallel, sequential, resource-aware |

## Scope and Tags

- **Bimanual-specific**: the method or benchmark is designed around two-arm coordination.
- **Bimanual-evaluated**: a broader robot-learning method with substantive bimanual experiments.
- `FM`: foundation/generalist model
- `VLA`: vision-language-action model
- `WM`: world model, video prediction, or predictive representation
- `Diffusion` / `Flow`: generative action modeling
- `IL`: imitation or behavior cloning
- `RL`: reinforcement learning
- `Planning`: task, skill, or motion planning
- `Real`: includes physical-robot evaluation
- `Sim`: simulation evaluation

## Contents

- [Surveys and Taxonomies](#surveys-and-taxonomies)
- [Foundation and Generalist Models](#foundation-and-generalist-models)
- [World Models and Generative Policies](#world-models-and-generative-policies)
- [Reasoning, Planning, and Skill Composition](#reasoning-planning-and-skill-composition)
- [Imitation Learning and Coordination Representations](#imitation-learning-and-coordination-representations)
- [Reinforcement Learning](#reinforcement-learning)
- [Humanoid and Dexterous Bimanual Learning](#humanoid-and-dexterous-bimanual-learning)
- [Datasets, Benchmarks, and Platforms](#datasets-benchmarks-and-platforms)
- [Related General Robot-Learning Methods](#related-general-robot-learning-methods)
- [Contributing](#contributing)
- [Acknowledgments](#acknowledgments)
- [Star History](#star-history)

## Surveys and Taxonomies

- **A Bimanual Manipulation Taxonomy**. *IEEE Robotics and Automation Letters, 2022.* [[paper](https://doi.org/10.1109/LRA.2022.3196158)] `Taxonomy` `Coordination`
- **Reinforcement Learning of Bimanual Robot Skills**. *Robot Learning, 2020.* [[book](https://link.springer.com/book/10.1007/978-3-030-26326-3)] `Survey` `RL`
- **A Survey of Dual-Arm Robotic Issues on Assembly Tasks**. *Robot Design, Dynamics and Control, 2019.* [[paper](https://doi.org/10.1007/978-3-319-78963-7_59)] `Survey` `Assembly`
- **Dual Arm Manipulation--A Survey**. *Robotics and Autonomous Systems, 2012.* [[paper](https://doi.org/10.1016/j.robot.2012.07.005)] `Survey`

## Foundation and Generalist Models

- **Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2605.30280)] `FM` `VLA` `Bimanual-evaluated` `Real` `Sim`
- **DeMaVLA: A Vision-Language-Action Foundation Model for Generalizable Deformable Manipulation**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2605.31286)] `FM` `VLA` `Deformable` `Real`
- **Mag-VLA: Vision-Language-Action Model for Bimanual Magnetically Actuated Microrobot Manipulation**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2605.28486)] `VLA` `Real`
- **A Pragmatic VLA Foundation Model**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2601.18692)] [[code](https://github.com/robbyant/lingbot-vla)] `FM` `VLA` `Multi-Embodiment` `Real` `Sim`
- **TwinVLA: Data-Efficient Bimanual Manipulation with Twin Single-Arm Vision-Language-Action Models**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2511.05275)] `FM` `VLA` `IL` `Real` `Sim`
- **ManiGaussian++: General Robotic Bimanual Manipulation with Hierarchical Gaussian World Model**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2506.19842)] [[code](https://github.com/April-Yz/ManiGaussian_Bimanual)] `FM` `WM` `Real` `Sim`
- **Towards a Generalizable Bimanual Foundation Policy via Flow-based Video Prediction**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2505.24156)] `FM` `WM` `Flow` `Real` `Sim`
- **Shake-VLA: Vision-Language-Action Model-Based System for Bimanual Robotic Manipulations and Liquid Mixing**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2501.06919)] `VLA` `Planning` `Real`
- **AnyBimanual: Transferring Unimanual Policy for General Bimanual Manipulation**. *ICCV, 2025.* [[paper](https://arxiv.org/abs/2412.06779)] [[project](https://anybimanual.github.io/)] `FM` `VLA` `IL` `Real` `Sim`
- **RDT-1B: A Diffusion Foundation Model for Bimanual Manipulation**. *ICLR, 2025.* [[paper](https://arxiv.org/abs/2410.07864)] [[project](https://rdt-robotics.github.io/rdt-robotics/)] [[code](https://github.com/thu-ml/RoboticsDiffusionTransformer)] `FM` `VLA` `Diffusion` `Real`
- **VoxAct-B: Voxel-Based Acting and Stabilizing Policy for Bimanual Manipulation**. *CoRL, 2024.* [[paper](https://arxiv.org/abs/2407.04152)] [[project](https://voxact-b.github.io/)] `VLA` `IL` `Real` `Sim`
- **Bi-VLA: Vision-Language-Action Model-Based System for Bimanual Robotic Dexterous Manipulations**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2405.06039)] `VLA` `Planning` `Real`

## World Models and Generative Policies

- **Morphologically Equivariant Flow Matching for Bimanual Mobile Manipulation**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2605.12228)] `Flow` `IL` `Real` `Sim`
- **Foundational World Models Accurately Detect Bimanual Manipulator Failures**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2603.06987)] `WM` `Safety` `Failure Detection` `Sim`
- **ManiFlow: A General Robot Manipulation Policy via Consistency Flow Training**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2509.01819)] [[project](https://maniflow-policy.github.io/)] `Flow` `IL` `Bimanual-evaluated` `Real` `Sim`
- **Diffusion-Based Imaginative Coordination for Bimanual Manipulation**. *ICCV, 2025.* [[paper](https://arxiv.org/abs/2507.11296)] [[code](https://github.com/return-sleep/Diffusion_based_imaginative_Coordination)] `WM` `Diffusion` `IL` `Real` `Sim`
- **D-CODA: Diffusion for Coordinated Dual-Arm Data Augmentation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2505.04860)] [[project](https://dcodaaug.github.io/D-CODA/)] `Diffusion` `Data Augmentation` `Real` `Sim`
- **Planning-Guided Diffusion Policy Learning for Generalizable Contact-Rich Bimanual Manipulation**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2412.02676)] [[project](https://glide-manip.github.io/)] `Diffusion` `Planning` `IL` `Real` `Sim`
- **FabricFlowNet: Bimanual Cloth Manipulation with a Flow-Based Policy**. *CoRL, 2021.* [[paper](https://proceedings.mlr.press/v164/weng22a.html)] [[project](https://sites.google.com/view/fabricflownet)] `Flow` `IL` `Deformable` `Sim`

## Reasoning, Planning, and Skill Composition

- **Bimanual Robot Manipulation via Multi-Agent In-Context Learning**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2604.20348)] `LLM` `Planning` `In-Context Learning` `Sim`
- **Learning to Plan & Schedule with Reinforcement-Learned Bimanual Robot Skills**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2510.25634)] `Planning` `Scheduling` `RL` `Sim`
- **Reflective VLM Planning for Dual-Arm Desktop Cleaning: Bridging Open-Vocabulary Perception and Precise Manipulation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2506.17328)] `VLM` `Planning` `Reflection` `Sim`
- **RoboPARA: Dual-Arm Robot Planning with Parallel Allocation and Recomposition Across Tasks**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2506.06683)] `LLM` `Planning` `Scheduling`
- **DAG-Plan: Generating Directed Acyclic Dependency Graphs for Dual-Arm Cooperative Planning**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2406.09953)] `LLM` `Planning` `Scheduling` `Sim`
- **Large Language Models for Orchestrating Bimanual Robots**. *Humanoids, 2024.* [[paper](https://arxiv.org/abs/2404.02018)] [[project](https://labor-agent.github.io/)] `LLM` `Planning` `Skill Composition` `Sim`
- **Efficient Bimanual Manipulation Using Learned Task Schemas**. *ICRA, 2020.* [[paper](https://arxiv.org/abs/1909.13874)] `RL` `Skill Composition` `Real` `Sim`
- **Learning and Composing Primitive Skills for Dual-Arm Manipulation**. *arXiv, 2019.* [[paper](https://arxiv.org/abs/1905.10578)] `IL` `Skill Composition` `Real`
- **A Certified-Complete Bimanual Manipulation Planner**. *IEEE T-ASE, 2018.* [[paper](https://doi.org/10.1109/TASE.2017.2780115)] `Planning`

## Imitation Learning and Coordination Representations

- **Ag2x2: Robust Agent-Agnostic Visual Representations for Zero-Shot Bimanual Manipulation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2507.19817)] `Representation` `Zero-Shot` `Sim`
- **Rethinking Bimanual Robotic Manipulation: Learning with Decoupled Interaction Framework**. *ICCV, 2025.* [[paper](https://arxiv.org/abs/2503.09186)] `IL` `Flow` `Representation` `Sim`
- **InterACT: Inter-dependency Aware Action Chunking with Hierarchical Attention Transformers for Bimanual Manipulation**. *CoRL, 2024.* [[paper](https://arxiv.org/abs/2409.07914)] [[project](https://soltanilara.github.io/interact/)] `IL` `Transformer` `Real` `Sim`
- **Bi-KVIL: Keypoints-based Visual Imitation Learning of Bimanual Manipulation Tasks**. *ICRA, 2024.* [[paper](https://arxiv.org/abs/2403.03270)] [[project](https://sites.google.com/view/bi-kvil)] `IL` `Representation` `Real`
- **Mobile ALOHA: Learning Bimanual Mobile Manipulation with Low-Cost Whole-Body Teleoperation**. *CoRL, 2024.* [[paper](https://arxiv.org/abs/2401.02117)] [[project](https://mobile-aloha.github.io/)] `IL` `Mobile Manipulation` `Real`
- **Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware**. *RSS, 2023.* [[paper](https://arxiv.org/abs/2304.13705)] [[project](https://tonyzhaozh.github.io/aloha/)] [[code](https://github.com/tonyzhaozh/aloha)] `IL` `ACT` `Real`
- **Stabilize to Act: Learning to Coordinate for Bimanual Manipulation**. *CoRL, 2023.* [[paper](https://arxiv.org/abs/2309.01087)] [[project](https://sites.google.com/view/stabilizetoact)] `IL` `Role Assignment` `Real`
- **Passive Bimanual Skills Learning from Demonstration with Motion Graph Attention Networks**. *IEEE RA-L, 2022.* [[paper](https://doi.org/10.1109/LRA.2022.3151173)] `IL` `Graph Network` `Real`
- **Robot Peels Banana with Goal-Conditioned Dual-Action Deep Imitation Learning**. *arXiv, 2022.* [[paper](https://arxiv.org/abs/2203.09749)] `IL` `Real`
- **Transformer-Based Deep Imitation Learning for Dual-Arm Robot Manipulation**. *IROS, 2021.* [[paper](https://arxiv.org/abs/2108.00385)] `IL` `Transformer` `Real`
- **Deep Imitation Learning for Bimanual Robotic Manipulation**. *NeurIPS Workshop, 2020.* [[paper](https://arxiv.org/abs/2010.05134)] `IL` `Real`

## Reinforcement Learning

- **COMBO-Grasp: Learning Constraint-Based Manipulation for Bimanual Occluded Grasping**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2502.08054)] `RL` `Self-Supervised` `Real` `Sim`
- **Efficient Bimanual Handover and Rearrangement via Symmetry-Aware Actor-Critic Learning**. *ICRA, 2023.* [[paper](https://irisli17.github.io/publication/icra23_bimanual/bimanual_handover.pdf)] `RL` `Symmetry` `Sim`
- **Bi-Manual Manipulation and Attachment via Sim-to-Real Reinforcement Learning**. *arXiv, 2022.* [[paper](https://arxiv.org/abs/2203.08277)] `RL` `Sim-to-Real` `Real` `Sim`
- **DAIR: Disentangled Attention Intrinsic Regularization for Safe and Efficient Bimanual Manipulation**. *ICLR, 2022.* [[paper](https://arxiv.org/abs/2106.05907)] [[project](https://mehooz.github.io/bimanual-attention)] `RL` `Safety` `Coordination` `Sim`
- **Bimanual Regrasping for Suture Needles Using Reinforcement Learning for Rapid Motion Planning**. *arXiv, 2020.* [[paper](https://arxiv.org/abs/2011.04813)] `RL` `Planning` `Surgical`
- **Exploiting Symmetries in Reinforcement Learning of Bimanual Robotic Tasks**. *IEEE RA-L, 2019.* [[paper](https://doi.org/10.1109/LRA.2019.2894624)] `RL` `Symmetry` `Sim`
- **Extracting Bimanual Synergies with Reinforcement Learning**. *IROS, 2017.* [[paper](https://doi.org/10.1109/IROS.2017.8206356)] `RL` `Synergy`

## Humanoid and Dexterous Bimanual Learning

- **DexMan: Learning Bimanual Dexterous Manipulation from Human and Generated Videos**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2510.08475)] `Humanoid` `Dexterous` `IL` `Video` `Sim`
- **HumanoidGen: Data Generation for Bimanual Dexterous Manipulation via LLM Reasoning**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2507.00833)] `Humanoid` `LLM` `Data Generation` `Sim`
- **Learning Diverse Bimanual Dexterous Manipulation Skills from Human Demonstrations**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2410.02477)] `Humanoid` `Dexterous` `RL` `IL` `Sim`
- **Bi-Touch: Bimanual Tactile Manipulation with Sim-to-Real Deep Reinforcement Learning**. *IEEE Robotics and Automation Letters, 2023.* [[paper](https://arxiv.org/abs/2305.09993)] `Tactile` `RL` `Sim-to-Real` `Real` `Sim`

## Datasets, Benchmarks, and Platforms

- **BiCoord: A Bimanual Manipulation Benchmark towards Long-Horizon Spatial-Temporal Coordination**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2604.05831)] [[project](https://buaa-colalab.github.io/BiCoord/)] `Benchmark` `Long-Horizon` `Coordination` `Sim`
- **BiManiBench: A Hierarchical Benchmark for Evaluating Bimanual Coordination of Multimodal Large Language Models**. *arXiv, 2026.* [[paper](https://arxiv.org/abs/2602.08392)] `Benchmark` `MLLM` `Planning` `Control`
- **RoboCOIN: An Open-Sourced Bimanual Robotic Data Collection for Integrated Manipulation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2511.17441)] [[project](https://FlagOpen.github.io/RoboCOIN/)] `Dataset` `Multi-Embodiment` `Real`
- **RoboEval: Where Robotic Manipulation Meets Structured and Scalable Evaluation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2507.00435)] [[project](https://robo-eval.github.io/)] `Benchmark` `Diagnostics` `Dataset` `Sim`
- **Benchmarking Generalizable Bimanual Manipulation: RoboTwin Dual-Arm Collaboration Challenge at CVPR 2025 MEIS Workshop**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2506.23351)] [[challenge](https://robotwin-benchmark.github.io/cvpr-2025-challenge/)] `Benchmark` `Real` `Sim`
- **RoboTwin 2.0: A Scalable Data Generator and Benchmark with Strong Domain Randomization for Robust Bimanual Robotic Manipulation**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2506.18088)] [[project](https://robotwin-platform.github.io/)] [[code](https://github.com/robotwin-Platform/robotwin)] `Benchmark` `Dataset` `Domain Randomization` `Sim-to-Real`
- **TWIN: Two-handed Intelligent Benchmark for Bimanual Manipulation (formerly PerAct2)**. *ICRA, 2025.* [[paper](https://arxiv.org/abs/2407.00278)] [[project](http://bimanual.github.io/)] `Benchmark` `VLA` `IL` `Sim`
- **Empowering Embodied Manipulation: A Bimanual-Mobile Robot Manipulation Dataset for Household Tasks**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2405.18860)] [[project](https://embodiedrobot.github.io/)] `Dataset` `Mobile Manipulation` `Real`
- **RoboTwin: Dual-Arm Robot Benchmark with Generative Digital Twins**. *CVPR, 2024.* [[paper](https://arxiv.org/abs/2404.13085)] [[project](https://robotwin-platform.github.io/)] `Benchmark` `Data Generation` `Sim`
- **The KIT Bimanual Manipulation Dataset**. *Humanoids, 2021.* [[paper](https://doi.org/10.1109/HUMANOIDS47582.2021.9555788)] [[dataset](https://motion-database.humanoids.kit.edu/)] `Dataset` `Human Motion`
- **Benchmarking Bimanual Cloth Manipulation**. *IEEE RA-L, 2020.* [[paper](https://doi.org/10.1109/LRA.2019.2956870)] `Benchmark` `Deformable` `Real`

## Related General Robot-Learning Methods

These papers are not exclusively about bimanual manipulation, but are frequently used as architectures, baselines, or conceptual foundations in bimanual work.

- **pi0.5: A Vision-Language-Action Model with Open-World Generalization**. *arXiv, 2025.* [[paper](https://arxiv.org/abs/2504.16054)] `FM` `VLA` `Bimanual-evaluated`
- **Fine-Tuning Vision-Language-Action Models: Optimizing Speed and Success**. *RSS, 2025.* [[paper](https://arxiv.org/abs/2502.19645)] [[project](https://openvla-oft.github.io/)] [[code](https://github.com/moojink/openvla-oft)] `VLA` `Fine-Tuning` `Bimanual-evaluated` `Real`
- **pi0: A Vision-Language-Action Flow Model for General Robot Control**. *arXiv, 2024.* [[paper](https://arxiv.org/abs/2410.24164)] `FM` `VLA` `Flow` `Bimanual-evaluated`
- **3D Diffusion Policy: Generalizable Visuomotor Policy Learning via Simple 3D Representations**. *RSS, 2024.* [[paper](https://arxiv.org/abs/2403.03954)] [[project](https://3d-diffusion-policy.github.io/)] `Diffusion` `IL` `Bimanual Baseline`
- **Diffusion Policy: Visuomotor Policy Learning via Action Diffusion**. *RSS, 2023.* [[paper](https://arxiv.org/abs/2303.04137)] [[project](https://diffusion-policy.cs.columbia.edu/)] `Diffusion` `IL` `Bimanual Baseline`

## Contributing

This project is actively maintained, and contributions are welcome through [pull requests](https://github.com/Destiny000621/awesome-bimanual-robot-learning/pulls) or [issues](https://github.com/Destiny000621/awesome-bimanual-robot-learning/issues). Missing papers, corrected metadata, code releases, project pages, and improved classifications are all useful contributions.

Please add papers only when they satisfy at least one criterion:

1. The method explicitly addresses bimanual or dual-arm coordination.
2. The paper introduces a bimanual dataset, benchmark, platform, or evaluation protocol.
3. A general robot-learning method reports substantive bimanual experiments and is clearly marked **Bimanual-evaluated**.

Use the following format:

```markdown
- **Paper Title**. *Venue, Year.* [[paper](URL)] [[project](URL)] [[code](URL)] `Tag1` `Tag2`
```

Please prefer the archival paper or arXiv abstract URL, verify the title and year, place the paper in its primary methodological category, and avoid duplicate entries.

## Related Collections

- [awesome-bimanual-manipulation](https://github.com/Skylark0924/awesome-bimanual-manipulation): broad collection covering learning, modeling, planning, control, teleoperation, devices, and applications.
- [Awesome RL for Multimodal Foundation Models](https://github.com/weijiawu/Awesome-RL-for-Multimodal-Foundation-Models): a large, actively maintained bibliography whose presentation and contribution workflow inspired parts of this repository.

## Acknowledgments

This repository builds on the community effort behind existing bimanual-manipulation bibliographies while focusing specifically on modern robot learning and foundation-model methods.

If this collection helps your research, please consider giving it a star and contributing missing work.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Destiny000621/awesome-bimanual-robot-learning&type=Date)](https://www.star-history.com/#Destiny000621/awesome-bimanual-robot-learning&Date)
