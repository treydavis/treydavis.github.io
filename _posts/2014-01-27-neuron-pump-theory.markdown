---
layout: post
title:  "Hydraulic Analogy for Neurons"
date:   2014-03-27
author: trey
categories: neuroscience ml neural-networks
---

When I learned about circuits, I often used the [Hydraulic analogy][ha] to reason with the problems. Batteries are pumps. Resistors are blocked up pipes. Capacitors are stretchy membranes. Inductors are massive fans. Since the metaphor is so graceful in that domain, I've decided to try and reason with neurons in the same way, since so much of their operation depends on movement of charge. It's worth noting that this is only a *model*, and not a true representation of how things work.

A neuron is like a sac of water that seizes up (fires) under 'certain conditions.' This produces a wave of water pressure ([action potential][ap]) rushing through the output pipe ([axon][a]). At the end of the pipe, it branches and forms many connections ([synapses][s]) with other sacs (neurons). The connections can vary in strength. Some will be clogged up and unresponsive. Others will transmit the flow freely.

The sacs maintain a certain internal pressure (resting potential) under normal conditions. The [membrane][m] that seals the sac has many pumps ([ion transporters][it]) that direct water inward, but they only when the pressure difference passes a certain threshold. Synapses will pump water into the sac, raising the pressure. As the pressure increases, the pumps begin to operate. If the synapses apply enough pressure, the pumps will have a compounding effect that raises the pressure suddenly (depolarization). This will continue until the pressure reaches the action potential, when the pumps will deactivate. This pressure pulse is shoved down the axon to the synapses and the process continues.

The most important variable that changes the operation of the neurons is how freely pressure is applied from a synapse ([synaptic plasticity][sp]). There are many theories for how this is changed. They are divided into two categories: strengthening flow ([long-term potentiation][ltp]) and weakening flow ([long-term depression][ltd]). These mechanisms are the keys to understanding how our brain is conditioned over time (memory).

[ha]: http://en.wikipedia.org/wiki/Hydraulic_analogy
[ltp]: http://en.wikipedia.org/wiki/Long-term_potentiation
[ltd]: http://en.wikipedia.org/wiki/Long-term_depression
[ap]: http://en.wikipedia.org/wiki/Action_potential
[a]: http://en.wikipedia.org/wiki/Axon
[s]: http://en.wikipedia.org/wiki/Synapse
[m]: http://en.wikipedia.org/wiki/Cell_membrane
[it]: http://en.wikipedia.org/wiki/Ion_transporter
[sp]: http://en.wikipedia.org/wiki/Synaptic_plasticity
