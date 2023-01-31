---
title: Literature Review: shape_servoing_of_deformable_objects_using_adaptive_deformation_model_estimation
author: Bardia Mojra
date: \today
geometry: margin=3cm
---

## Meta Data

- Title:
- Authors:
- Institution:
- Journal: IFAC
- Year: 2023

## Summary

### How do you rate your own level of confidence in the subject of the submission that you have been asked to review?

Very confident

### Contribution

- Please assess the contribution of this submission
- Theoretical contribution: Minor
- Technological contribution: None
- Survey/tutorial contribution: Minor
- Originality of concepts: Minor
- Thoroughness of results: Questionable
- Importance of results: Questionable
- Awareness of the literature: Good
- Style and clarity: Major

## Comments to the editorial staff

The paper is clear on their approach, but the authors need to address the problem of deformable object shape servoing at its core. The open problem regarding deformable object state estimation is characterized by
a high-dimensional chaotic system, not a nonlinear one. Many researchers seem to miss that.

The authors make no mention of chaotic or nonlinear systems
in their writing.

They assume the system at hand is nonlinear, and its linearized representation is guaranteed to exist. Unfortunately, this is not true for chaotic systems.
They showed a good understanding of adaptive controller design but not chaotic systems. However, I doubt the method yields better performance than the gradient-based adaptive control approach on never-seen tasks, and I would like to see more experimental data and evidence to support their claims.

## Comments to the authors

In this paper, the authors present a framework for shape servoing of deformable objects using adaptive control. They present a good review of the existing literature on this topic.

Effectively, they perform system identification to obtain the deformation Jacobian matrix and deploy an ICL-based (integral concurrent learning) adaptive controller to servo the object.

In the main contributions section, please clarify what you mean by "without requiring a prior knowledge about the model." This statement contradicts their assumptions. Moreover, the authors left out important information regarding the space of the obtained Jacobian matrix. They used radial basis function (not functions), picked the rank (perhaps through experimentation), and made no comments about the intrinsic coordinate frame of this space. It is in contradiction with the "no prior knowledge" statement. I would not make such a claim.

Moreover, through their assumptions, they reduced a high-dimensional chaotic system control problem to a high-dimensional nonlinear system control problem. How often does the proposed method beat the baseline method in the simulation? How is the prior data related to performance?

The proposed method is novel and contributes to the research community, but more evidence is needed to support the superior performance claim.
