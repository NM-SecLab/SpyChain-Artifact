# SpyChain Artifact (Anonymous Repository)

## Open Science Artifacts

### Artifacts Provided
To support evaluation of our work, we provide the following materials:

- **Pseudocode and diagrams** illustrating the structure of malicious and defensive cFS components, including communication flow, trigger conditions, and mitigation logic.  
- **Screenshots and representative logs** from the NOS3 simulation and COSMOS ground station, showing telemetry traces and attack/defense outcomes corresponding to figures and tables in the paper.  
- **Documentation and methodology** sufficient to reproduce the scenarios *in principle* using the public NOS3 release, which is already open source and widely available.  

---

### Access During Review
At submission time, pseudocode, screenshots, and example logs are hosted here in this anonymized repository. These materials are scrubbed of identifying metadata and are sufficient for reviewers to verify the plausibility of our design, methodology, and reported results.

---

### Limitations and Responsible Disclosure
We deliberately **do not** release the complete source code of the malicious components. Because many operational spacecraft use cFS or closely related software, releasing flight-ready malware would pose a direct security risk.  

Instead, we provide high-level pseudocode and partial interfaces that illustrate functionality without enabling immediate weaponization. Defensive modules and mitigation strategies are fully described.  

We also do not redistribute NOS3 itself, as it is already available as an open-source NASA project. Our contribution lies in how NOS3 can be configured and extended, not in modifying or repackaging the simulator.  

---

### Post-Acceptance Plan
If the paper is accepted, we are open to sharing full component code and experiment scripts **with trusted collaborators under controlled conditions**, with the aim of improving defenses for flight software. This approach balances reproducibility with the responsibility to prevent the distribution of weaponizable code.

---
