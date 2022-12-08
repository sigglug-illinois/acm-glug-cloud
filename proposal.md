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

Basic web applications can be supported through compute engine that manages user-defined VMs.

- We can run [yggdrasil](https://github.com/acm-uiuc/yggdrasil) (ACM auth and user-service) in docker-compose on a VM.
  - Likewise, the resume book application.
- We can offer IRC bouncers by giving individual users a VM.
- We can offer GPU training by giving SIGs a VM scheduled on a node with GPU access.

However, future applications should be written at a higher level using platform-as-a-service or function-as-a-service. This allows us to consolidate common services. Instead of each application having their own database, we could deploy one shared distributed RDBMS instance, and give users different views on that database. This saves compute overhead, and also deduplicates maintenance effort.

Likewise, scheduling each user's GPU training in its own VM leads to scheduling overhead and inefficient sharing of resources. Instead, we could use a job scheduler like SLURM.

Therefore, we will offer IaaS VMs first, while we build out more specialized services as needed later.

- Compute engine (aka IaaS)
  - This is the most general but least optimized compute platform.
  - We could offer each user a small VM to use as a sandbox.
  - OpenStack Nova implements a compute engine.
- Function-as-a-service (aka FaaS or serverless compute)
  - This is useful for HTTP web applications and microservices.
  - We would offer a FaaS service for predefined languages and environments.
- Relational database (aka SQL)
  - This is useful for web applications to store structured data (yggdrasil uses Postgres).
  - OpenStack Nova implements a compute engine.
  - We would probably manage an instance of Postgres by hand. OpenStack Trove implements a database provisioner, should we want to allow users to create their own databases.
- Object store (aka S3)
  - This is useful for web applications to store unstructured data.
  - We could host a Nix binary cache. This would accelerate ACM projects that use Nix to install dependencies.
  - OpenStack Swift implements an object store.
- Batch job scheduler
  - This is for offline transaction processing, including GPU-accelerated training.
  - SLURM implements a batch job scheduler with GPU capability.
- Virtual desktops
  - This provides a Linux desktop environment for those who do not have access to a Linux machine. Most of the time, we would prefer users use a VM, but for graphical applications, users can provision a desktop environment.
- CI/CD runner
  - GitHub CI has a limited free tier, but they allow users to host their own runner to run the CI/CD workflow. We can host some low-priority VMs these for our users.

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
