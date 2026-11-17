--- 
# 1. Denario Project
Interesting background, using LLMs to help scientific discovery. Give ideas on what new research avenues can be investigated, using the entire Denario pipeline. Reproduce the paper utilizing Open source Qwen3.8 125B. Supervised by c1 goat boris. Work includes using the Denario pipeline to generate some papers that we will compare with the frontier model's outputs.
# 2. Tropical Cyclones
Utilizing machine learning on climate data to help detect cyclones. Highly industry oriented and is in collaboration with the catastrophe team at INIGO insurance, with potential visits to their london office. Uses a new package called TCTrack for the analysis. Probably best for fluid dynamics backgrounds or high interest in climate, so prob not for me but still.
# 6. Gaussian Video
Gaussian splatting has been used to fit to images. Here we extend the idea to video. As no official code for the paper has been released, the goal of the paper is to reproduce the paper results and build our own implementation of the paper's ideas using tools such as `gsplat` and `torchdiffeq`. Also this is from the department of engineering, which could be a potential avenue for phd if I am interested.
# 7. Black Hole Image
Simply put, lets use the publicly available data to check how reproducible this image is. Pretty cool project, but tbh not too sure ab its use industry wise or experience wise. Feels a bit too niche.
# 8. Satellite Streak detection
Goal is to implement a type of CNN called U-net, typically used for biomedical imaging. Relevant to computer vision type jobs, think medical imaging, remote sensing and computer vision in general. Though admittedly the project feels a bit too easy, since its only implement it. Though a lot of time is needed to train it. The extension is also a bit lacklustre since its only implementing it again on a different dataset. Though I do match the requirements very well, even if theyre a bit easy to match.
# 9. Radio Galaxy Morphologies
Most interesting part is the use of self upervised learning and representation learning.
# 12. Search for $\chi_{c1}(3872)$ Meson and its Properties
Similar to SHP but more advanced, and we will learn to use ROOT. Cool and interesting for particle physics work, however relatively irrelevant to other fields. I meet requirements relatively well, but I am not familiar with angular momenta in quantum mechanics, or rather I forgor.
# 14. Machine Learning for Predicting LaTeX Compilation Workload
Topic itself is a bit bland, but methodology is interesting. Includes work with transformers, graph/tree based models\method\data?
# 15. Federated Learning for Medical Imaging
Uses NVIDIA FLARE framework to simulate hospital nodes and then testing different federated learning strategies to combat client drift.
# 21. Hidden Coordinates of the Cosmic Web
Very hard, recent open problem which could potentially lead to a publication. Based on representation learning of embedded parameters? Symbolic learning
# 22. LHCb Flavour tagging 
Uses DeepSet neural networks. Potential cern membership to utilize LHCb resources.
# 23. Artificial Neural Networks to model particle detection effects
Supervised by matt kenzie, highly related work to particle physics. Focuses on using gaussian processes and artificial Neural networks. These approaches are widely used in other fields, but relatively unexplored in HEP.
# 24. Sweight densities
also by matt kenzie, more focused on statistical methods, particularly on constraining sweights to [0,1] and solving the issue that sweights can be negative.
# 27. Deep Learning Inference for Gravitational Wave Detection
Essentially using neural posterior estimation to map the waveform for the gravitational wave. Probabilistic machine learning, useful for industry. Priscilla is the supervisor.
# 28. Neural Networks to Rediscover General Relativity
In particular by looking at binary black holes spiralling into each other. The key publication shows that a neural network can do so. Combination of physical modelling and machine learning, potentially useful for quant roles. Priscilla is the supervisor.
# 30. Simulation Based Inference for Galaxy Spectra
Traditionally this is done using bayesian techniques such as MCMC or nested sampling, but this is super expensive computationally. Instead we can use SBI to train a neural density estimator on simulated observations. Then the neural network can estimate the densities for the actual datasets
# 33. Extreme tropical cyclone detection with ai weather models
Ai weather models by NVIDIA, google deepmind, huawei and other players of that sort already outperform the traditional physics based forecasts. But the question remains open on whether they can predict gray swan events. But its weather so whatever, kinda meh
# 34. AI agents in physics
similar to denario project, but with other thigns idk, useful but fuck is it a boring topic.
# 36. Hubble tension
Hubble constant is in tension based on 2 different measurements, global vs local. Project focuses on analyzing cepheid data to replicate this resultsd. i.e. pulsating stars. Extra work is investigating sensitivity of results to various choices made when handling the data.
# 37. Calabi Yau metrics via symbolic regression
calabi yau metrics are rarely known, ml can approximate them tho. Then we try using symbolic regression to extract, compact interpretable results. A globally valid closed-form metric is an ambitious extension.
# 39. QFT Lean
Using lean to formalize QFT, and mathlib and physlib
# 40. Learning Compositional grammar across languages
Uses latent variable models, dynamic programming and probabilistic graphical models. Probably one of the best projects for an industry role. differentiable structured inference, unsupervised learning.
# 41. Learning compositional types through neuro symbolic ccg induction
Very similar to 40. Same supervisor. Provides experience in deep latent variable learning, neuro-symbolic modelling and differential dynamic programming. Another crazy good project for industry. Honestly all of weiwei sun's projects are sick.

# Overall Thoughts
Since the goal is likely to go into experimental particle physics for a PhD, the idea should be to pick those. There are 5 HEP related projects overall.
- LHCb flavour tagging
- ANNs for particle detection effects
- Search for the $\chi_{c_{1}}(3872)$ meson and its properties
- Converting sWeights to probabilities with density ratios
- Calabi-Yau metrics via symbolic regression
Now, the first 3 are the most appropriate as they are directly related to exp-HEP, whereas the other 2, one is more focused on statistical methods and them testing them on HEP situations. The other, is more for theoretical physics I think, since it involves trying to calculate Calabi-Yau metrics.

The idea for ranking them, is I should put the projects that have PhD supervisors as the priority, so flavour tagging, 
