### Abstract

We propose a ACM/GLUG cloud. The cloud would be built from donated and surplus machines and adminstered by volunteer ACM members. Our goal is to provide members with real-world server administration experience, and provide ACM SIGs and projects with compute resources (free or less expensive than AWS).

### Operation

- We will use the server room (3103) for physical storage, power, and internet.
- We will use declarative infrastructure-as-code.
  - Collaborate without direct access to the server.
  - The software configuration persists even as physical machines are added and removed.
- The cluster will be administered by a committee volunteers who have final say on design decisions.
- We will leverage open-source off-the-shelf software as much as possible.
  - [OpenStack](https://www.openstack.org/software/)
- We will use a credit based system to encourage frugal but full use of the resources.

### Resource offering

Additionally, we may try to support the following higher-level software services:

  - Virutal machine compute engine
  - Container/kubernetes cluster
  - Function-as-a-service (aka serverless compute)
  - Relational database
  - Public access (or member only) UNIX server, like SDF server or hashbang.sh
  - Object storage (aka S3)
  - IRC bouncer
  - RDP access to virtual Linux desktops
  - Batch job scheduler for offline transaction processing (including GPU resources)
  - https://charm.sh/
  - Nix/Bazel/CCache build farm
  - Static site hosting
    - Host GNULUG
    - Host member webspaces
    - Host mirrors
  - Dynamic site hosting
    - [yggdrasil](https://github.com/acm-uiuc/yggdrasil)
    - Member webspaces
    - Other ACM infra webapps
  - VCS hosting (GitLab, sourcehut)
  - GitLab/GitHub CI workers
    - Make sure we don't duplicate the universities offering here
  - Host Matrix or RocketChat

Services tentatively not offered:

- Static site serving
  - This is necessary for many web applications  [JAM stack](https://www.cloudflare.com/learning/performance/what-is-jamstack/).
  - However, GitHub pages offers free, optimized static site serving through their exensive CDN.
- Container engine
  - This offers little advantage over compute engine where the user runs a container.
- Distributed stream-processing
  - This supports online processing and streaming data analytics.
  - However, it is also a complex and rarely needed service.
- NFS
  - Use object-store instead. Object-store has more advanced metadata management.
- Container image service
  - Ideally, users would use Nix rather than Docker. This permits more sharing and deduplication that docker layers do not.
  - Where container image stores are really necessary, one could use an object-store as a container image service.

### UX

Users could interface to our cloud in two ways:

1. Through a web portal, which is easiest to get started.
  - [OpenStack Horizon](https://www.openstack.org/software/releases/yoga/components/horizon) implements a web UI.
2. Through a third-party deployment tool that can deploy a cloud architecture on multiple clouds, so the user's configuration would not be vendor-locked to the ACM/GLUG cloud.
  - For example [Terraform](https://terraform.io) or [CloudFoundry](https://www.cloudfoundry.org/), support AWS, GCP, Azure, and OpenStack.
  
We would host a static documentation site explaining the resources, limitations, and frequently asked questions.

Users could create issues in our GitHub tracker for support.

### Resource Alocation

- Consumers have an account with credits that they can use to bid on resources. They can submit a curve that bids higher for the first unit than for the second, reflecting diminishing marignal utility.
- Prices are set dynamically by supply and demand.
  - If requests are less than supply of some resource, that resource is free. We satisfy all requests.
  - If requests are greater than supply of some resource, then the price should be set to the greatest price such that the bids less than that price are satisfiable.
- Consumers earn credits if they donate or lease a machine according to the price that the resources are sold at during that period.
  - If one is out of credits, they are incentivized to donate or lease a machine to our cloud. We can let them use their machine while also keeping it used while it would otherwise be idle.
  - At the same time, the committee of volunteers can create more credits to give, for example, to give a small provision to each user. However, if they do this too much, it reduces the incentive to contribute to the cluster. The committee should ensure that the price of buying and donating resources is less than just renting those resources on commercial clouds, considering our goal is to provide users with inexpensive compute resources.
- Ideally, these resources would not be used for research projects with affiliated faculty where the faculty have their own resources.

### Interested parties

- GLUG: Sam
- Infra: Steven, Andro
- SIGAIDA: Jlevine18
- SIG Ecom: Dan, Phil
- GWC: Rutvik
