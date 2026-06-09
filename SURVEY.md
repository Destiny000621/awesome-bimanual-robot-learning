# A Survey of Robot Learning for Bimanual Manipulation

This survey synthesizes the papers curated in [Awesome Robot Learning for Bimanual Manipulation](https://github.com/Destiny000621/awesome-bimanual-robot-learning). It is intended as a living field map rather than a complete historical review. The focus is on learning-based bimanual and dual-arm manipulation, including foundation models, VLA policies, world models, diffusion and flow policies, imitation learning, reinforcement learning, task planning, datasets, and benchmarks.

## Abstract

Bimanual manipulation requires more than producing two streams of robot actions. A capable robot must decide when two arms should act independently, when they should coordinate tightly around a shared object, when one arm should stabilize while the other acts, and when actions must be sequenced because of shared workspace, contact, or resource constraints. Recent work has moved from task-specific dual-arm controllers toward foundation policies, language-conditioned planners, world models, generative policies, and scalable simulation benchmarks. However, the field still lacks a unified account of how perception, high-level reasoning, temporal scheduling, reusable skill execution, verification, and recovery should interact in general bimanual systems. This survey organizes current work around system role, learning paradigm, policy family, and coordination structure, then identifies open problems for scalable real-world bimanual robot learning.

## 1. Scope

Robot learning for bimanual manipulation sits at the intersection of manipulation learning, embodied reasoning, motion planning, and multi-agent coordination. The papers in this repository are included when they satisfy at least one of three criteria:

1. The method explicitly addresses bimanual or dual-arm coordination.
2. The work introduces a bimanual dataset, benchmark, platform, or evaluation protocol.
3. The method is broader than bimanual manipulation but reports substantive bimanual experiments and is useful as a baseline or foundation.

This survey emphasizes four questions:

- How should bimanual coordination be represented?
- How should high-level planners compose low-level learned policies?
- How do learned policies generalize across tasks, objects, layouts, embodiments, and domains?
- How should bimanual success, efficiency, safety, and recovery be evaluated?

## 2. A Taxonomy for Bimanual Robot Learning

Existing surveys and taxonomies establish that bimanual manipulation is not a single problem class. Tasks differ in contact structure, coupling strength, role asymmetry, and temporal dependence. The following taxonomy is useful for interpreting modern learning-based systems.

| Axis | Main Options | Typical Questions |
|---|---|---|
| Coordination regime | independent parallel, loosely coupled, tightly coupled, asymmetric support-action, sequential shared-resource | Can both arms act at the same time, or must one wait? |
| System architecture | monolithic bimanual policy, twin unimanual policies, high-level planner plus skills, model-based controller | Where is coordination represented? |
| Learning signal | imitation learning, reinforcement learning, self-supervision, post-training, synthetic data generation | What supervision teaches coordination? |
| Policy family | VLA, diffusion, flow matching, transformer action chunking, world model policy, classical planner | What model produces actions or plans? |
| Evaluation target | success, collision-free success, makespan, idle time, resource violations, recovery, OOD generalization | What does the benchmark reward beyond completion? |

This taxonomy exposes a central tension: policies that directly model both arms can learn tight coordination, but they may require task-specific demonstrations and scale poorly. Systems that compose reusable single-arm policies can scale better, but they need explicit planning, scheduling, verification, and resource management to avoid inefficient or unsafe execution.

## 3. Foundation and Generalist Models

Recent foundation-model work attempts to learn broad manipulation capabilities from large and diverse datasets. For bimanual manipulation, these methods are important because they promise reuse across tasks, embodiments, and environments.

Representative systems include [RDT-1B](https://arxiv.org/abs/2410.07864), [AnyBimanual](https://arxiv.org/abs/2412.06779), [TwinVLA](https://arxiv.org/abs/2511.05275), [VoxAct-B](https://arxiv.org/abs/2407.04152), [Bi-VLA](https://arxiv.org/abs/2405.06039), [Shake-VLA](https://arxiv.org/abs/2501.06919), [Qwen-VLA](https://arxiv.org/abs/2605.30280), and [A Pragmatic VLA Foundation Model](https://arxiv.org/abs/2601.18692). These papers differ in whether they train a bimanual policy directly, transfer unimanual models, use voxelized action representations, or rely on language-conditioned action generation.

The main strength of this line is broad visuomotor generalization. Foundation policies can absorb heterogeneous data and execute language-conditioned tasks without designing a separate controller for every manipulation primitive. This is especially useful in bimanual settings where the same low-level skills, such as reaching, grasping, placing, inserting, opening, and closing, appear across many tasks.

The main limitation is that broad policies do not automatically solve high-level bimanual task management. A model may know how to pick and place objects, but still fail to decide which arm should act first, when both arms should work in parallel, how to avoid a shared rack insertion conflict, or when to stop and recover after a failed subtask. In other words, foundation policies help with action generation, but they do not remove the need for explicit scheduling, state verification, and failure handling.

## 4. World Models and Generative Policies

World models and generative policies provide a second path toward general bimanual behavior. Instead of only predicting actions, these systems can model future states, contact outcomes, visual changes, or action distributions. This is attractive for bimanual manipulation because coordination often depends on anticipating whether an arm will block a region, whether an object has been inserted, whether a container is open, or whether a failure has occurred.

Representative work includes [ManiGaussian++](https://arxiv.org/abs/2506.19842), [Towards a Generalizable Bimanual Foundation Policy via Flow-based Video Prediction](https://arxiv.org/abs/2505.24156), [Foundational World Models Accurately Detect Bimanual Manipulator Failures](https://arxiv.org/abs/2603.06987), [Diffusion-Based Imaginative Coordination for Bimanual Manipulation](https://arxiv.org/abs/2507.11296), [D-CODA](https://arxiv.org/abs/2505.04860), [Planning-Guided Diffusion Policy Learning for Generalizable Contact-Rich Bimanual Manipulation](https://arxiv.org/abs/2412.02676), [Morphologically Equivariant Flow Matching for Bimanual Mobile Manipulation](https://arxiv.org/abs/2605.12228), and [FabricFlowNet](https://proceedings.mlr.press/v164/weng22a.html).

Generative policies are strong for modeling multimodal action distributions and smooth trajectories. Diffusion and flow policies have become common baselines for manipulation because they can represent diverse demonstrations and produce temporally coherent action chunks. World models add another capability: predicting the consequences of actions. In bimanual settings, this can support progress estimation, failure detection, and recovery.

However, most existing systems do not yet expose world models as typed, reusable execution tools with bounded horizons and structured feedback. A promising direction is to treat world-model executors as a tool family: each invocation specifies a skill label and a grounded instruction, then the tool returns actions, predicted terminal state, progress, uncertainty, and success or failure evidence. This structure can connect low-level generalization with high-level task planning.

## 5. Reasoning, Planning, and Skill Composition

High-level planning is essential when bimanual tasks involve temporal dependencies, shared resources, and conditional execution. Recent work has explored language-model planning, dependency graphs, parallel allocation, task schemas, and skill composition.

Key examples include [DAG-Plan](https://arxiv.org/abs/2406.09953), [RoboPARA](https://arxiv.org/abs/2506.06683), [Large Language Models for Orchestrating Bimanual Robots](https://arxiv.org/abs/2404.02018), [Reflective VLM Planning for Dual-Arm Desktop Cleaning](https://arxiv.org/abs/2506.17328), [Bimanual Robot Manipulation via Multi-Agent In-Context Learning](https://arxiv.org/abs/2604.20348), [Learning to Plan & Schedule with Reinforcement-Learned Bimanual Robot Skills](https://arxiv.org/abs/2510.25634), [Efficient Bimanual Manipulation Using Learned Task Schemas](https://arxiv.org/abs/1909.13874), [Learning and Composing Primitive Skills for Dual-Arm Manipulation](https://arxiv.org/abs/1905.10578), and [A Certified-Complete Bimanual Manipulation Planner](https://arxiv.org/abs/1705.02573).

This line of work directly studies the question that pure action policies often leave implicit: how should a robot decide the order, arm assignment, and parallelization of subtasks? Dependency-graph methods are especially relevant because they can represent predecessor constraints and expose opportunities for parallel execution. LLM and VLM planners add semantic flexibility, allowing plans to be generated from language, visual state, and task context.

The open challenge is generality. Some planning systems are demonstrated on a small number of tasks or assume fixed low-level skills. Others produce plausible high-level plans but lack robust execution feedback. Scalable bimanual systems need planners that can produce typed programs with resource locks, preconditions, success predicates, failure predicates, recovery policies, and safe termination conditions, while remaining compatible with reusable learned executors.

## 6. Imitation Learning and Coordination Representations

Imitation learning remains one of the strongest paradigms for real-world bimanual manipulation because teleoperation data can capture contact-rich behavior, role assignment, and coordinated motion. Influential systems include [Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware](https://arxiv.org/abs/2304.13705), [Mobile ALOHA](https://arxiv.org/abs/2401.02117), [InterACT](https://arxiv.org/abs/2409.07914), [Stabilize to Act](https://arxiv.org/abs/2309.01087), [Bi-KVIL](https://arxiv.org/abs/2403.03270), [Transformer-Based Deep Imitation Learning for Dual-Arm Robot Manipulation](https://arxiv.org/abs/2108.00385), [Deep Imitation Learning for Bimanual Robotic Manipulation](https://arxiv.org/abs/2010.05134), [Passive Bimanual Skills Learning from Demonstration with Motion Graph Attention Networks](https://ieeexplore.ieee.org/document/9720487), [Goal-conditioned Dual-Action Imitation Learning](https://arxiv.org/abs/2203.09749), [Ag2x2](https://arxiv.org/abs/2507.19817), and [Rethinking Bimanual Robotic Manipulation](https://arxiv.org/abs/2503.09186).

These papers show several ways to represent bimanual behavior: action chunking, keypoints, hierarchical attention, graph attention, role decomposition, decoupled interaction, and agent-agnostic visual representations. A recurring insight is that bimanual manipulation is often structured, not merely high-dimensional. One arm may stabilize an object while the other manipulates it; two arms may perform symmetric movements; or both arms may execute independent object transfers until they contend for a shared placement region.

The limitation is that imitation quality is bounded by demonstrations. Human teleoperation may be safe and feasible but not time-optimal. In many bimanual tasks, expert demonstrations underuse parallelism because humans naturally serialize actions, avoid risky simultaneous motions, or operate one arm more cautiously. This creates an opportunity for learned planners to improve efficiency by discovering when parallel execution is safe while preserving sequential ordering when constraints require it.

## 7. Reinforcement Learning

Reinforcement learning has been used to learn bimanual coordination, symmetry-aware control, safe attention, grasping, handover, regrasping, and sim-to-real manipulation. Representative papers include [DAIR](https://arxiv.org/abs/2106.05907), [Bi-Manual Manipulation and Attachment via Sim-to-Real Reinforcement Learning](https://arxiv.org/abs/2203.08277), [COMBO-Grasp](https://arxiv.org/abs/2502.08054), [Bi-Touch](https://arxiv.org/abs/2307.06423), [Efficient Bimanual Handover and Rearrangement via Symmetry-Aware Actor-Critic Learning](https://irisli17.github.io/publication/icra23_bimanual/bimanual_handover.pdf), [Exploiting Symmetries in Reinforcement Learning of Bimanual Robotic Tasks](https://ieeexplore.ieee.org/document/8637816), [Extracting Bimanual Synergies with Reinforcement Learning](https://doi.org/10.1109/IROS.2017.8206356), and [Bimanual Regrasping for Suture Needles](https://arxiv.org/abs/2011.04813).

RL is attractive when successful behavior is hard to demonstrate or when the desired behavior is more efficient than available demonstrations. It can optimize makespan, coordination, safety margins, or task reward directly. Symmetry and role structure can also reduce sample complexity by exploiting the relationship between the two arms.

The main barrier is scalability. Bimanual RL can be expensive because the action space is large, contact dynamics are complex, and sparse rewards are common. Many RL systems are therefore task-specific. A promising compromise is to use RL or preference optimization at higher levels, such as scheduling or tool selection, while relying on post-trained reusable executors for bounded low-level skills.

## 8. Benchmarks, Datasets, and Platforms

The field is increasingly shaped by benchmarks and data generators. Important resources include [RoboTwin](https://arxiv.org/abs/2409.02920), [RoboTwin 2.0](https://arxiv.org/abs/2506.18088), the [RoboTwin Dual-Arm Collaboration Challenge](https://arxiv.org/abs/2506.23351), [PerAct2](https://arxiv.org/abs/2407.00278), [BiCoord](https://arxiv.org/abs/2604.05831), [ST-BiBench](https://arxiv.org/abs/2602.08392), [RoboCOIN](https://arxiv.org/abs/2511.17441), [RoboEval](https://arxiv.org/abs/2507.00435), [Empowering Embodied Manipulation](https://arxiv.org/abs/2405.18860), [The KIT Bimanual Manipulation Dataset](https://doi.org/10.1109/HUMANOIDS47582.2021.9555788), and [Benchmarking Bimanual Cloth Manipulation](https://ieeexplore.ieee.org/document/8957044).

These benchmarks matter because they define what the field measures. Early bimanual evaluation often focused on whether a task was completed. Newer benchmarks include long-horizon tasks, domain randomization, multimodal coordination, data generation, and diagnostic evaluation. RoboTwin 2.0 is particularly relevant for studying generalization under randomized layouts, object instances, viewpoints, and dual-arm task structures.

Future benchmarks should report more than success rate. For bimanual manipulation, important metrics include collision-free success, task makespan, arm idle time, both-arms-progress ratio, shared-resource violations, recovery success, failure-classification accuracy, and in-distribution versus out-of-distribution performance.

## 9. Cross-Cutting Trends

### 9.1 From Monolithic Policies to Structured Systems

The field is moving from single task-specific policies toward structured systems that combine perception, planning, learned skills, and verification. Monolithic bimanual policies can be powerful, but they often entangle task logic and motor execution. Structured systems can expose reusable components, making it easier to evaluate whether failure comes from perception, scheduling, execution, or recovery.

### 9.2 From Completion to Efficiency

Many bimanual tasks have multiple valid executions. A sequential strategy may succeed but waste the second arm. An efficient policy should parallelize independent subtasks while sequencing actions that contend for a shared resource. This shifts evaluation from binary success to temporally grounded measures such as makespan, idle time, and resource conflicts.

### 9.3 From Open-Loop Execution to Verification and Recovery

Long-horizon bimanual tasks are vulnerable to small errors. A vial may be grasped poorly, a cabinet may remain partially closed, a bowl stack may be unstable, or an object may block a shared insertion area. Closed-loop verification is therefore critical. Planners need to verify preconditions and terminal states, classify failures as recoverable or unrecoverable, and decide whether to retry, reassign arms, retreat, reset, or terminate safely.

### 9.4 From Task-Specific Skills to Reusable Tool Families

Several strands of work suggest a tool-like interface between planners and robot policies. The key idea is to expose bounded, reusable skills rather than train a separate end-to-end policy for every bimanual task. For bimanual manipulation, a reusable executor family might include reaching, grasping, moving held objects, placing, inserting, opening, closing, and retreating. The planner then composes these skills with arm assignments, dependencies, and shared-resource locks.

## 10. Open Problems

### Generalizable Bimanual Task Management

Current planners can generate dependency graphs or orchestrate skills, but many are still evaluated on narrow task families. The field needs task managers that generalize across object categories, layouts, arm assignments, resource conflicts, and recovery situations.

### Invocation-Aligned Low-Level Executors

Foundation policies and world models are often trained for broad action generation, but high-level planners need reliable bounded invocations. A low-level executor should understand a typed command, execute for a finite horizon, and return interpretable feedback about progress, uncertainty, and terminal state.

### Shared-Resource-Aware Scheduling

Many practical bimanual tasks contain a mixture of parallelizable and sequential subtasks. Examples include multi-object insertion into one rack, scanning objects through a single scanner, packing items into a narrow tray, using one fixture for capping, or replenishing through a narrow opening. These tasks require explicit resource locks and temporal constraints.

### Demonstration Inefficiency

Human teleoperation demonstrations are not necessarily optimal. Demonstrators may serialize actions that could safely run in parallel. Learning systems should therefore distinguish feasibility demonstrations from optimal schedules, then improve efficiency using scheduling preference data, simulation rollouts, or structured reward signals.

### Robust Real-World Generalization

Real bimanual systems face domain variation in object pose, lighting, viewpoint, object identity, friction, calibration, and perception noise. Benchmarks and methods should evaluate whether policies remain safe and efficient under these variations, not only whether they solve a fixed scripted setup.

### Standardized Metrics

Success rate alone hides important differences between methods. A stronger evaluation protocol should include:

- task success and collision-free success;
- makespan and arm idle time;
- both-arms-progress ratio;
- resource-lock violations;
- verification accuracy;
- recoverable and unrecoverable failure classification;
- recovery success rate;
- in-distribution and out-of-distribution performance.

## 11. Implications for Future Systems

A scalable bimanual robot-learning system will likely be hierarchical. At the top level, a multimodal reasoning planner should parse the scene, decompose the task, assign arms, schedule parallel groups, enforce shared-resource constraints, and verify state transitions. At the lower level, reusable learned executors should perform bounded manipulation skills and report structured feedback.

This architecture offers a middle path between purely monolithic bimanual policies and brittle hand-coded pipelines. It can reuse single-arm or skill-specialized policies while still modeling the coordination structure that makes bimanual manipulation difficult. The most important research question is not only whether two arms can complete a task, but whether the system can decide when to parallelize, when to sequence, and how to recover when execution diverges from the plan.

## 12. Suggested Reading Path

For a fast entry into the field:

1. Start with taxonomy and survey papers to understand coordination regimes.
2. Read ALOHA, Mobile ALOHA, InterACT, Stabilize to Act, and Bi-KVIL for imitation learning and representation.
3. Read RDT-1B, AnyBimanual, TwinVLA, VoxAct-B, and Qwen-VLA for foundation and VLA policies.
4. Read DAG-Plan, RoboPARA, LLM orchestration, and learned planning-and-scheduling work for high-level reasoning.
5. Read ManiGaussian++, diffusion/flow bimanual policies, and world-model failure-detection papers for generative and predictive approaches.
6. Use RoboTwin, RoboTwin 2.0, PerAct2, BiCoord, ST-BiBench, and RoboCOIN to understand current benchmark coverage.

## 13. Maintaining This Survey

This document should evolve with the repository. When adding a new paper, consider updating:

- the relevant methodological section;
- the taxonomy if the paper introduces a new coordination pattern;
- the benchmark section if the paper adds tasks or metrics;
- the open problems if the paper resolves or reframes a limitation.

The goal is to keep the survey useful for researchers who want to understand not only what papers exist, but how the field is moving.
