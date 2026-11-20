Microservices & Containerisation BSE 4105 – 2026/1 

Alex Mwotil 

1 

### What We'll Cover 

**1** 

**Monolithic Architectures** 

How we used to build everything 

**2** 

**Microservice Architectures** 

Small services, independently run 

**3** 



<!-- Start of picture text -->
Containerisation<br><!-- End of picture text -->

OS-level virtualisation and orchestration 

**4** 

###### **Docker** 

Images, containers and Dockerfiles 

2 

## Monolithic Architectures 

One codebase, one deployment, one fate 

3 

### What Is a Monolith? 

###### Applications have often been packaged as monoliths. 

##### **Defining traits** 

##### **What that leads to** 

All required functionality in a single codebase Built on the MVC framework — classical 3-tier Evolves through incremental growth 

Highly coupled internally 

Complexity increases with every feature One change can affect anything The whole thing ships together The whole thing fails together 

**A monolith is not a mistake — it is the right starting point for most systems. The problems come later, with scale.** 

4 

The Classical Three Tiers Presentation, functional and persistence layers. 

**Presentation** The mobile app or web front end the user actually touches **Functional /** The business logic, served by a web server, often exposed **Logic** over REST **Persistence** Usually a single relational database 

**Scaled by cloning the whole application behind a load balancer.** 

5 

### A Real System: APDD 

Automated Plant Disease Diagnosis — near real-time, in-field diagnosis for cassava. 

**Used by hundreds of farmers across East Africa and by national agricultural research organisations. Five components** 

**S3 · S4 · Mobile app S1 · Pest ID S2 · Surveys Diagnosis Prediction** AI plant Identifies Forecasts disease app Field survey Rapid plant pests from disease in the collection diagnosis imagery spread farmer's hand 

_We'll build this as a monolith first, then decompose it._ 

6 

### APDD as a Monolith 

One codebase, one web server, one database. 



<!-- Start of picture text -->
Mobile<br>app<br><!-- End of picture text -->

**Web server — single deployment S1 S2 S3 S4** Relational database 

**What works** Simple to develop and deploy at first One place to look for anything 

**What binds you** S1–S4 share one codebase and one database They must be released together 

7 

### Scaling a Monolith 

You cannot scale one part — you clone the entire application. 



<!-- Start of picture text -->
Load<br>balancer<br>Full application Full application Full application<br>S1 S2 S3 S4 S1 S2 S3 S4 S1 S2 S3 S4<br>every copy carries all four every copy carries all four every copy carries all four<br>Only S3 is under load — but you pay for three more<br>copies of S1, S2 and S4. Operational overhead and<br>resource wastage.<br><!-- End of picture text -->

8 

### Where Monoliths Hurt 

> ✕ **DevOps is hard** Introducing agile delivery practices needs a major refactor first 

**Resource** ✕ **wastage** 

You run components you did not need more of 

> ✕ **Build bottleneck** A large codebase becomes a performance bottleneck of its own 

**Operational overhead** 

✕ 

More to deploy, monitor and keep consistent 

###### **All-or-nothing** ✕ **scaling** 

Scale the entire codebase to add redundancy or handle load 

> ✕ **Tight coupling** One team's change can break another team's feature 

9 

# Microservice Architectures 

An application as a suite of small, independent services 

10 

### What Is a Microservice Architecture? 

#### **Develop an application as a suite of small services.** 

**Agility** Change direction without a rewrite 

**The focus Simplicity** Each service is small enough to hold in your head 

**Scalability Speed** Scale only the part Develop and deploy under load faster 

###### **Motivated by** 

**The scalable cloud** Capacity on demand made small services practical 

**Market dynamics** New features have to ship fast, or someone else ships them 

11 

### Properties of a Microservice 

Each service complies with the Single Responsibility Principle: do one thing, and do it well. 

✓ ✓ ✓ ✓ **Owns its own data Autonomous Fault isolated Lightweight** ✓ ✓ ✓ **Business-capability Independently Easy to monitor specific deployable** 

**Small enough to do one thing well — but a service that owns nothing is just overhead.** 

12 

APDD Decomposed The four functional units become loosely coupled microservices. 



<!-- Start of picture text -->
Mobile app<br>S1 S2 S3 S4<br>Pest ID Surveys Diagnosis Prediction<br>each service writes to its own data store<br>Services expose their functionality over REST, RPC or<br>SOAP.<br><!-- End of picture text -->

13 

### Independently… 

###### The whole point: these four axes stop being coupled. 

**1 2 3 Developed Deployed Scaled** Each service can Ship S3 on Add capacity only use a different Tuesday without where the load programming touching S1, S2 or actually is stack S4 **Compare with the monolith: every one of these had to happen to the whole application at once.** 

**3 4 Scaled Maintained** Add capacity only A team can own a where the load service end to actually is end 

14 

### How Big Should a Microservice Be? 

There is no line count — these are the practical tests. 

**Two weeks to an MVP** 

**A two-pizza team** 

Small enough that a minimum viable version is ready in a fortnight **Three weeks to onboard** 

No bigger than a team you could feed with two pizzas — roughly 5 to 8 people 

**But not too small** 

A new developer should be productive on it within three weeks 

If you routinely change two services together, they should be one service 

**too big  →  a monolith again** 

**too small  →  all overhead** 

15 

### The Trade-offs 

###### Microservices move complexity — they do not remove it. 

**Network communication** 

Calls that were function calls are now network calls, with latency and failure 

**Less code reuse** 

Shared logic gets duplicated across services 

**Management complexity** 

Many services to deploy, version, secure and observe 

**Global testing** 

Testing and debugging across service boundaries is genuinely harder 

**Data consistency** 

No single database means no single transaction 

**Operational maturity** 

You need CI/CD and monitoring in place before this pays off 

_Source: orientsoftware.com_ 

16 

### Monolith vs. Microservices 

Neither is correct in the abstract — it depends on where you are. 

###### **Choose a monolith when** 

**Choose microservices when** 

_early, small, or uncertain_ 

_scale and team pressure arrive_ 

The team is small and co-located 

The domain is still changing shape 

Different parts need different scaling Multiple teams block each other on release 

You have no CI/CD or monitoring yet Simplicity is worth more than independence 

You need independent technology choices You already have the operational maturity 

**Most successful microservice systems started as a monolith that was decomposed — not built that way on day one.** 

17 

## Containerisation 

Packaging a service with everything it needs to run 

18 

### Virtualisation 

###### How we got here. 

**1** 

**Servers got powerful** Far more capacity than one workload needed 

**2** 

**Emulate a machine** It became possible to run a machine inside another 

**3 Many OSes, one box** Multiple operating systems on a single piece of hardware 

**4 And the cloud** Rent that capacity by the hour instead of buying it 

**Containerisation is a particular type of virtualisation — so it helps to know what it is a type of.** 

19 

### What Is Containerisation? 

Operating system virtualisation. 

#### **The underlying OS is shared by many containers.** 

**Each container is limited** 

**Each container carries** 

Its resources are capped 

Its libraries 

Its view of the system is restricted 

Its dependencies 

It cannot see the other containers 

Its environment variables 

**Containers can run directly on hardware, or on top of hardware virtualisation — both are common.** 

20 

### Hardware vs. OS Virtualisation 

Same goal, different layer — and a very different weight. **Hardware virtualisation OS virtualisation (containers)** 

**App  ·  App  ·  App App  ·  App  ·  App Guest OS   Guest OS   Guest OS Container engine Hypervisor  (e.g. KVM) Host operating system Host operating system Physical hardware Physical hardware** **_no guest OS — that is the saving_ HV needs a hypervisor. OV needs a container engine running on the host OS.** 

21 

### Hardware vs. OS Virtualisation, Compared 

###### **Hardware virtualisation** 

###### **OS virtualisation** 

**Operating system** 

A different OS for each instance 

**One shared OS for many instances** 

**Start-up time** 

Minutes or more 

**Seconds or less** 

**Portability** 

**Resource footprint** 

Can be moved between machines 

Large 

**Easily moved between VMs or physical machines Small** 

_Seconds instead of minutes is what makes containers viable for CI/CD pipelines._ 

22 

### Container Orchestration 

Automating the deployment and management of containerised applications. 

**Automated rollout** 

Push a new version across the fleet — and roll it back if it misbehaves 

**Health monitoring** Notice when a container dies, and replace it 

**Scaling** Add and remove instances as load changes 

**Resilience** Keep the declared state true, even as machines fail 

**Kubernetes is the dominant orchestrator** 

You declare the state you want — how many replicas, which image — and it works to keep reality matching that declaration. 

23 

### Microservices & Containers Together 

Two different things that happen to fit each other perfectly. 

**Microservices** An architectural design pattern 

**Containers +** A deployment technology 

**A container is a packaging and deployment technology for a microservice Loosely Lighter Independent Observable coupled** A smaller, less The boundary is Deploy one Easy to monitor resourceenforced, not just service without and to scale intensive process agreed the others 

**Observable** Easy to monitor and to scale 

24 

Docker 

Build once, run anywhere 

25 

### What Is Docker? 

**An open-source platform that packages an application and its dependencies into a standard unit — a container.** 

**Lightweight** A process, not a whole machine 

**Portable** The same unit moves between environments 

**Isolated** Runs without interference from its neighbours 

**Consistent** Behaves the same everywhere it runs 

```
build once, run anywhere
```

26 

### Docker Architecture 

##### Five pieces you will meet constantly. 

###### **Docker** 

###### **Docker Client** 

The CLI tool you type into. Sends commands to the engine. 

###### **Daemon** 

Background service managing containers, images, networks and volumes. 

**Docker Engine** 

The core component that creates, ships and runs containers. 

###### **Docker Image** 

The static basis of a container — represents a full application. 

###### **Docker Registry** 

Stores images — Docker Hub, or a private registry. 

**You type into the Client  →  the Daemon does the work  → Images come from and go to the Registry** 

27 

### Images vs. Containers 

The single most important distinction in Docker. 

**Image** 

##### **Container** 

_the static thing_ 

_the running thing_ 

Represents a not-running application Contains everything the app needs to run 

The standard unit the service runs in 

Derived from an image 

Built from a Dockerfile Immutable — you rebuild, you don't edit 

Isolated from other containers 

One container per app or service 



<!-- Start of picture text -->
docker<br>run<br>image container<br><!-- End of picture text -->

28 

### Build · Ship · Run 

The whole Docker workflow in three verbs. 



<!-- Start of picture text -->
1 2 3<br>Build Ship Run<br>Turn a Dockerfile into an  Push that image to a  Start a container from the<br>image registry image<br>docker build docker push docker run<br>A Dockerfile lives with your source code and is versioned with it — so<br>images are 100% reproducible.<br><!-- End of picture text -->

29 

### Getting an Image 

Pull it down from a registry, then see what you have. 

```
$docker pull mikegcoleman/catweb:1.0
```

Pulls the 1.0 version of the catweb image from the mikegcoleman repository on Docker Hub to your local host. 

```
$docker images
```

Lists every image on your Docker host. 

**An image name is repository/name:tag. Leave the tag off and Docker assumes :latest.** 

30 

### Running a Container 

```
docker run -d -p 5000:5000 --name catweb
$
mikegcoleman/catweb:latest
```

**`-d`** Detached — run in the background Map port 5000 on the host to port 5000 in the **`-p 5000:5000`** container **`--name`** Name the container. Omit it and Docker invents one **`catweb`** for you 

```
$docker ps
```

_Shows running containers.  docker ps -a shows stopped ones too._ 

31 

Stopping & Cleaning Up Containers and images are removed separately. 

```
$docker stop catweb
```

Stops a running container. It still exists — it is just not running. 

```
$docker rm catweb
```

Removes the stopped container. Add -f to forceremove a running one. 

```
$docker rmi
mikegcoleman/catweb:latest
```

Removes the image itself. 

**You can always use the container ID instead of the name.** 

32 

Building & Publishing Creating your own image and sharing it. 

```
$ docker build -t mikegcoleman/catweb:2.0 .
```

**-t names the image** Repository and name Plus a version tag — here 2.0 

**The . at the end** 

Build from the Dockerfile in this directory Or give an explicit path instead 

```
$ docker push mikegcoleman/catweb:2.0
```

The opposite of pull — sends your new image up to the registry. 

33 

### Docker Command Reference 

**`docker pull`** Download an image from a registry **`docker images`** List images on this host **`docker run`** Start a new container from an image **`docker ps`** List running containers  (-a for all) **`docker stop`** Stop a running container **`docker rm`** Remove a stopped container **`docker rmi`** Remove an image **`docker build`** Create an image from a Dockerfile **`docker push`** Upload an image to a registry 

_Add --help to any of these to see the full set of options._ 

34 

### The Dockerfile 

Instructions for building an image — a mix of ordinary Linux commands and Docker keywords. 

**Lives with your code** 

Committed to the repository alongside the application 

**Version controlled** Pipeline and image changes are reviewed like any other change 

**100% reproducible** Anyone can rebuild the identical image from it 

**Worth optimising** Order the instructions well and rebuilds get much faster 

**This is where containers differ from VMs** Virtual machines are often hand-built. Lose the golden image and you are stuck. A Dockerfile means the image can always be rebuilt from source. 

35 

### A Dockerfile, Line by Line 

###### A simple Flask web application. 

```
FROMalpine:latest
RUNapk add --update py-pip
RUNpip install --upgrade pip
COPYrequirements.txt /usr/src/app/
RUNpip install -r
/usr/src/app/requirements.txt
COPYapp.py /usr/src/app/
COPYtemplates/index.html
/usr/src/app/templates/
EXPOSE5000
CMD["python", "/usr/src/app/app.py"]
```

Start from the official Alpine **`FROM`** Linux base image Install Python and pip, then **`RUN`** upgrade pip Copy the requirements list **`COPY`** in, then install the libraries Copy the application code **`COPY`** and templates into the image Declare that the app listens **`EXPOSE`** on port 5000 What to run when the **`CMD`** container starts 

```
COPY
COPY
EXPOSE
```

_Every instruction runs against the image being built — not against your local machine._ 

36 

### Optimising a Dockerfile 

Each instruction creates a layer, and layers are cached. 

###### **Do this** 

###### **Avoid this** 

Put things that rarely change near the top Copy requirements.txt before the app code Combine related RUN commands into one layer Start from a small base image such as Alpine 

Copying the whole project before installing deps A separate RUN for every single command 

Leaving build tools in the final image Baking secrets into any layer — they persist 

**Copy your dependency list before your source code — then editing a source file doesn't re-install every library.** 

37 

### Recap & Exercise 

**What we covered** 

**Your exercise** 

✓ 

Monoliths — and where they hurt 

> ✓ Write a Dockerfile for a small web app 

> ✓ Microservices, and their trade-offs 

> ✓ Containerisation vs virtual machines Docker images, containers and ✓ Dockerfiles 

> ✓ Build it and run it locally 

> ✓ Push the image to a registry 

> ✓ Add a docker build job to your pipeline 

**Connect it up: your Docker build belongs in the .gitlab-ci.yml that we looked at last week** 

38 

