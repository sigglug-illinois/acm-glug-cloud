# Meeting, Wednesday September 9, 2023

* Participants:
  * Sam Grayson
  * Tren Hao
  * Nathan Somers
  * Jake Levine
* What names should we settle on?
  * GLUG/Infra cluster
* Purpose and offerings of the other cluster and of our cluster?
  * HPC cluster: batch execution for SIG{AIDA, Ecom, HPC}
    * SIGAIDA also has fleshed out requirements, but could be computationally intensive
      * NCSA compute cluster may be a better option
  * Container execution cluster: general purpose, SIGPWNY, SIGAIDA, ACM Infra, ACM Projects
    * SIGPWNY has the most fleshed out requirements
    * ACM Projects Committee Saurav & Max leads
    * For our cluster: offer container engine, maybe VM space. We don't have many nodes and only 1 GPU.
* What IPAM network for each of us to use?
  * Could use same
* What level of collaboration going forward?
  * Get requirements documents from other SIGs, especially SIGAIDA and SIGPWNY
  * Raw k8s access could be acceptable user interface/service offeirng
* Next steps:
  * GLUG/Infra cluster team:
    * What we want to do
      * Revise task list
        * Emphasize doing container engine first
    * How we're going to do it
      * Make them all have the same distro
      * Find candidate HTTP/HTTPS service, ask Engr IT to open external port for that service
      * Deploy persistent storage for k8s
      * Deploy k8s
  * Jake:
    * Send us requirements docuemnts from SIGAIDA, SIGPWNY, Infra, Applications, others...
    * forward infra-compute applications over
