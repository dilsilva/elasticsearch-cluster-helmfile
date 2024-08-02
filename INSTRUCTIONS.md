# Home assignment: Infrastructure Engineer @ Picnic

_Target time: 6-8 hrs_

## Context

The Run team, responsible for the last-mile delivery service of Picnic’s supply
chain, has reached out to the Infrastructure team for help with a new project.

To better monitor the quality of their services, the Run team is looking for a
system via which they can (near) real-time query and visualize the free form
reviews that customers fill out after each delivery.

The Run and Infrastructure teams came together for a design session and came to
the conclusion that ES (Elasticsearch) would be a good fit: the Run team already
has prior experience with ES and ES is capable of handling the volume and
free-form nature of the data.

## Requirements

During the design session, the following requirements were identified:

- The ES cluster must be deployed in a K8s (Kubernetes) cluster.
- The Run team already owns a K8s cluster, so provisioning a K8s cluster is not
  a part of the requested solution.
- The ES cluster can be deployed using any tool to manage K8s workloads: vanilla
  manifests, CRDs, Helm charts, kustomize, etc.
- The ES cluster’s configuration must ensure availability of the ES cluster
  during failures in the underlying hardware and regular maintenance operations
  in the K8s cluster.
- The ES roles assigned to each of the ES nodes must be identical for all nodes
  in the ES cluster.
- The solution is shared with the Run team via either a zip-file or a Git(Hub)
  repository containing everything to deploy an ES cluster.
- The solution contains a README, explaining:
  - How the solution should be used to deploy the ES cluster.
  - What design decisions have been made in this solution (cluster
    configuration, used tools, etc.).
- The solution is functional and results in a running ES cluster if the README
  instructions are followed.

## In summary

With all requirements on paper, it's now up to you to implement a stable and resilient solution, that will be easy to use for the Run team.

Please include a SOLUTION.md file. In it, explain why you made certain design and implementation choices. This helps us understand your intentions and thought process better during review.
Ensure coverage of the following key areas in this file, although it is not mandatory to incorporate all of them into the initial solution, as some may be seen as future enhancements:
 - Deliberate on the deployment method—whether it be through plain YAML, Helm, Kustomize, or any other suitable mechanism.
 - Outline how the solution will handle potential failures to maintain continuous service availability.
 - Elaborate on authentication, authorization, encryption, and any other security practices/concerns used in this solution.
 - Plan for ongoing operational tasks such as system upgrades, cluster scaling, disaster recovery procedures, etc. Explain your approach to handling these day-to-day operational challenges.
 - Draft a strategy for system observability, specifying which metrics are critical for monitoring and analyzing the system's health and performance.
 - Additional Future Improvements.
We value your way of thinking, so try to avoid copying and pasting from other solutions or other resources/LLM models. If you want to use them, please put a reference.

Good luck, and have fun!
