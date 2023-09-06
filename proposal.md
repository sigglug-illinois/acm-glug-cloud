# Infra/GLUG cluster

## Abstract

We propose a Infra/GLUG cluster.
The cloud would be built from surplus, donated, and specially-purchased machines and adminstered by volunteers.
Our goal is to provide members with real-world server administration experience, and provide ACM SIGs, committees, and projects with compute resources for non-misison-critical applications (free or less expensive than AWS).

## Hardware

Most of our current hardware was previously acquired for the pre-COVID cluster.
Members may elect to let us borrow hardware (especially if they do no have the space, cooling, or rack space to run it in their dorm).

See our [inventory](https://docs.google.com/spreadsheets/d/1Mex7f6qN9uSypg3oOCucHvvdE0HO6KnUJdlAhtJ2QbY/edit#gid=928936190).

## Service offering

One possible service offering is a _container engine_ or a _virtual machine (VM) engine_.
Containers share more resources than VMs, which makes them faster to spin up and more scalable at the cost of greater flexibility and security of VMs.
A _distributed container engine_ can launch containers on one of many nodes in a cluster; Distributed container engines set routing and domain name resolution rules, so users don't need to know or care where their container is running.
Kubernetes (k8s) is the most popular distributed container engine.

Here is an example of some services that can be implemented in a container engine:

- Static sites such as binary mirrors, binary caches
- Public access UNIX server space (like SDF or Hashbang.sh)
- Hosting SIG, project's, or user's dynamic sites
  - [yggdrasil](https://github.com/acm-uiuc/yggdrasil)
- Version-control repositories (Git, Mercurial, DARCS with or without frontends like GitLab, Gitea, SoftServe)
- Build-farm
- Matrix bridges
  - I see no reason to move our homeserver from matrix.org. However, we could host bridges that are otherwise not available.
- Etherpad
- Pastebin
- Grpahical Linux virtual workspace
  - Could provide workspace for Girls Who Code.
- CI workers
- IRC bouncer
  - I personally don't use IRC as much anymore now that a lot of people are switching to Matrix.

A VM engine could support even more applications:

- Public access UNIX server space with more freedom
- Testing Linux From Scratch
- Testing/staging new cluster configuration
- Testing alternative container engines (CRI-o)
- Testing (not virtual) filesystems

However, implementing a VM engine involves manipulating the hypervisor, and I have less direct experience with that.
Perhaps, if after the container engine is successful, we can 

We might benefit from consolidating commonly used services:

- SQL server
- Key-value cache
- Reverse proxy
- Object storage
- Function-as-a-service (aka serverless compute)
- Batch job scheduling

## UX

Users could interface to our cloud by using the Kubernetes API, especially through the `kubectl` client.
For example,

```bash
$ ssh sam-grayson@cluster.acm.illinois.edu
You are now logged in to the cluster

$ kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: foobar-application
spec:
  containers:
  - name: nginx
    image: nginx:7.0
    env:
      - name: FOO_BAR_CONFIG_VAR
        value: "spam & eggs"
    resources:
      requests:
        cpu: "1"
        ram: 1G
  # Other containers used by foobar-application go here.
```

Kubernetes will map this container to a node with enough capacity to serve the request of 1 CPU and 1G of RAM.

Kubernetes supports role-based access-control, so we can give each user the least-privilege they need to accomplish their task.

## Networking

Nodes in the cluster can talk to any other node on the Illinois internal network.
Publicly serving sites entails dealing with Engineering IT.
However, Engineering IT does not at present permit incoming connections. There are a few ways to address this issue:

1. Request a that the UIUC/Illinois Firewall simply does not filter incoming connections to us, and then we do it ourself.
   It would likely be very difficult to convince them that we are able to setup a secure SSH server since there are very high-level orders to not permit incoming conections, in particular SSH connections. 
2. Use [Cloudflare tunnels](https://www.cloudflare.com/products/tunnel/) as a way of bypassing NAT.
   Cloudflare tunnels run a daemon on our servers that opens multiple redundant conectionks to Cloudflare's datacenters, then Cloudflare's network accepts incoming connections on our behalf and forwards them.
   This product is specifically designed to deal with firewalls such as that of UIUC.
   The free version can tunnel several protocols, including HTTP, HTTPS, and SSH.
   This gives the advantage that websites or other HTTP services taht we host are completely freely accessible without specifical client configuration.
   SSH does require some client configuration if we do not use the premium version of Cloudflare tunnels.
   A sponsorship *may* be possible to get this premium version for free as a sponsorship, however they generally prefer to sponsor groups with a different profile from ours (major FOSS projects and groups that suffer from censorship).
3. Rent a VPS (such as OVH, or DigitalOcean; many providers exist) and use it in essentially the same way as Cloudflare Tunnels.
   Options to do this on the software end include SSH tunnels (open SSH connection from our cloud to the VPS with -R), GRE tunnels, or mesh networking (e.g., Slack's Nebula).
   It would be preferable to use a VPS provider with a good network and unlimited bandwith for this, so OVH is a good option.
   DigitalOcean, however, offers free student credit.
   We can use [Nebula](https://github.com/slackhq/nebula) for virtual intranet.

## Resource Alocation

In the beginning, we may not really care too much about resource allocation.
If one user is submitting expensive jobs, we may ask them to stop or apply resource limitations on all users.

In later stages, we may use a system of credits.

## Interested parties

- GLUG
- Infra committee
- SIGAIDA
- SIG Ecom
- SIG HPC
- SIG PWNY
- GWC
