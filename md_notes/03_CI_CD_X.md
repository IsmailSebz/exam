Continuous Integration & Delivery BSE 4105 – 2026/1 

Alex Mwotil 

1 

## What We'll Cover 

**1** 

**Continuous Integration** 

Merge and verify continuously 

**2** 

**Build & Test Automation** 

The engine that makes CI work 

**3** 

**4** 

**Continuous Delivery CI/CD with & Deployment GitLab** 

Getting it safely Pipelines, YAML to production and runners 

2 

Continuous Integration Merging everyone's work, continuously and safely 

3 

## Why Integration Is Hard 

Software systems are complex — and teams make them more so. 

**The problem** 

### **The instinct** 

- A minor edit can break the whole system Many developers at once compounds it Long-lived branches drift from master The longer you wait, the worse the merge 

- "I'll branch to keep master clean" 

- Fine — if the branch is short-lived Otherwise you are deferring the pain 

- And the conflict grows every day 

**Integration pain grows with time. The fix is to integrate more often, not less.** 

4 

## The Integration Loop 

Every change travels the same path — CI is about shortening it. 

**Design Develop Integrate Test Release feedback — the shorter this loop, the faster you learn Our goals Integrate continuously Minimize time Test continuously** between the phases not once a sprint every single change 

5 

## What is Continuous Integration? 

### **Regularly build, test and merge code changes into the main branch.** 

**What the team does** 

**What the machine does** 

Members integrate their work frequently 

Multiple integrations per day 

Automatically builds every change Runs the test suite against it 

Introduce small changes to the code 

Integrates it into the shared repository 

Constantly review code in the repository 

Reports back — fast 

**A practice for identifying integration errors fast — each integration is automatically verified.** 

6 

**“** Continuous Integration is a software development practice where each 

member of a team merges their changes into a codebase together with their colleagues' changes at least daily. Each of these integrations is verified by an automated build (including test) to detect integration errors as quickly as possible. 

_Teams find that this approach reduces the risk of delivery delays, reduces the effort of integration, and enables practices that foster a healthy codebase for rapid enhancement with new features._ 

###### **Martin Fowler** 

**7** 

## CI Is a Practice, Not a Tool 

_You can install Jenkins tomorrow and still not be doing CI._ 

**A practice** 

**A behaviour change** 

**A daily habit** 

What you DO — not what you use/install 

It asks people to work differently 

It changes a developer's routine, every day 

**The tooling is the easy part.** A team that commits once a week to a long-lived branch has not adopted CI, no matter how good its pipeline is. 

8 

Always Keep master Working You should always have a working version of the system. 



<!-- Start of picture text -->
commit → build → test<br>✓ Tests pass ✕ Tests fail<br>Congratulations — master still  Fix it immediately. A broken<br>works. Carry on. master blocks the whole team.<br><!-- End of picture text -->

9 

## Small Changes, As Frequently As Possible 

CI depends on small changes. Big-bang merges defeat the whole point. 

**Small changes** 



easy to integrate · fast feedback · clear impact 

**One large change** hard to review · slow feedback · which bit broke it? 

**Easy to integrate** Less to conflict with 

**Fast to verify** The build finishes quickly **AFAP — as frequently as possible.** 

**Clear feedback** You know which change broke it 

10 

## Why CI? 

> ✓ **Less risky releases** Automated testing and integration catch problems early 

> ✓ **Small iterations** 

Push small changes and iterate continually 

> ✓ **Better productivity** More automation, less context switching 

> ✓ **Better visibility** Everyone can see the state of the product 

> ✓ **Faster delivery** Ship features and fix bugs sooner 

> ✓ **Always deployable** There is always a shippable version available 

11 

## CI Best Practices 

**1** 

**Commit early & often** 

Incremental development — every commit is an integration point. 

**2** 

##### **Branch for features** 

Know when to branch, and keep branches short-lived. 

**3** 

**Integrate on all branches** Every branch gets CI, not just master. 

**4** 

**Branch & tag strategy** 

Agree it as a team and write it down. 

**Short-lived branches are the single highest-leverage habit on this list.** 

12 

## Two Branching Models 

Both work with CI — they trade off speed against control. 

#### **Trunk-Based Development** 

#### **Git Flow** 

_Everyone on one branch, open access_ 

_One develop branch, strict access_ 

All developers work on master directly 

Short-lived feature branches only 

Branches must compile and pass all tests 

Developers branch off develop PR → comments → review → accept → merge When develop matures, cut a release branch 

Merged straight back to master 

Test and fix, then merge to master 

Truly continuous — conflicts stay small 

More control, more ceremony 

_Source: toptal.com_ 

13 

## The CI Tools Landscape 

##### **Jenkins** 

Open-source automation server. The most widely deployed. Written in Java, ~1800 plugins. **`jenkins.cranecloud. io`** 

##### **GitLab CI/CD** 

Built into GitLab. Runners execute jobs defined in .gitlabci.yml. **`our focus today`** 

**GitHub Actions** Launched 2018. Event-driven workflows, free for public repositories. 

##### **CircleCI** 

Cloud-based. Triggered on code change; mobile, web, API and serverless. 

**We used to run a Jenkins instance at jenkins.cranecloud.io — but our exercises use GitLab CI/CD.** 

14 

# Build & Test Automation 

The engine that makes continuous integration possible 

15 

## What Is a Software Build? 

##### **A process that turns source code and developer artifacts into a product customers can run.** 

**Compile Package Installers Test** Source code, in Compress targets Generate the Run the automated compiled languages into JAR, ZIP or WAR software installers tests against the like Java or C++ archives users run build 

**Build automation is a basic component of continuous integration.** 

_Source: sealights.io_ 

16 

## Build Automation 

What the pipeline does on every commit. 

**1 2 Trigger Build** on a dedicated on every commit server 

##### **Practices** 

Build every commit, or as often as possible Keep the environment consistent and replicable Build every branch, not just master 

**3 4 5 Test Publish Review** unit tests and artifacts to a metrics and more repository feedback 

##### **Build tools** 

Make · Ant · Maven (mvn) Gradle · MSBuild Whatever your language ecosystem uses 

17 

## Test Automation 

```
build fast · test fast · fail fast
```

_Test automation is at the core of CI/CD._ 

#### **Types of test** 

#### **Methodologies** 

Unit testing — the TDD level Integration testing System testing 

White box — you can see the code Black box — you cannot Grey box — a bit of both 

**C / C++ Web** check · CUnit · Selenium CppUnit 

**Python Ruby** pytest · nose Cucumber · RSpec 

18 

## Why Automate Tests? 

**Catch regressions** 

#### **Faster feedback** 

**Cheaper fixes** 

Ensure code changes don't introduce bugs 

Far quicker than waiting on manual testing 

Small, fresh code is easier to fix than old code 

**Reliable results** Replicable — the same test, the same answer 

#### **Scalable** 

Run tests in parallel across many machines 

#### **Confidence** 

The team trusts master enough to release from it 

**Manual testing still matters — automation frees humans to look for the faults machines can't imagine.** 

19 

Continuous Delivery & Deployment Getting verified changes safely into production 

20 

## What CI Gives Us 

Before we go further — this is what continuous integration already does for you. 

**Ties together** 

The builds and the tests, on every change 

**Archives Automates** Artifacts, test Build triggers and results and build the pipelines logs themselves 

**Gates** Merges can be blocked; changes can be staged 

**So we have a verified, working build. Now what?** Getting that build in front of real users is the job of Continuous Delivery and Continuous Deployment. 

21 

## Delivery vs. Deployment 

Both are "CD" — the difference is who presses the last button. 

##### **Continuous Delivery** 

##### **Continuous Deployment** 

_Automated up to a production-LIKE environment_ 

_Automated all the way INTO production_ 

Latest stable version goes to a test environment 

Every change that passes goes to production 

That environment mimics production closely Ensures the product could be deployed at any time 

- A human decides when it actually ships 

No human gate at the end 

The team focuses on building the product Deployment becomes a routine non-event 

**Delivery makes release possible at any time. Deployment makes it happen automatically.** 

22 

## The Full Pipeline 

Each stage extends the automation a little further to the right. 



<!-- Start of picture text -->
Commit Build Test Staging Production<br>Continuous Integration<br>Continuous Delivery<br>Continuous Deployment<br><!-- End of picture text -->

_The only difference between the last two bars is the human involvement_ 

23 

## The Six Principles of CD 

#### The goal: release software that works any time, in any environment. 



<!-- Start of picture text -->
1 Label assets 2 Clean environment 3 Label each build<br>4 Run all tests 5 Feedback reports 6 Rollback<br>Underneath all six: automated, repeatable builds and automated, repeatable tests.<br><!-- End of picture text -->

24 

## Label Assets · Clean Environment 

- **1 · Label assets of a repository** 

- **2 · Produce a clean environment** 

Identify and track every asset 

Historical tracking of files and file groups 

OS and its configuration Server components — app, database, messaging 

Makes rollback to an old version possible 

Server configuration itself 

Lets you take meaningful snapshots 

Third-party tools and web frameworks 

Remove and reapply software, scripts and configuration values to confirm the environment behaves as expected. 

25 

## Label Each Build · Run All Tests 

#### **3 · Label each build** 

#### **4 · Run ALL the tests** 

A unique identifier for every build 

The repository code needs a label 

Unit tests through to functional tests On the build machine and a production replica 

The act of building needs its own label Labels uniquely identify the binary output 

Confidence that the software really works Manual testing still finds new faults 

```
0.1_mac.dmg
```

_a build label can carry the target platform_ 

26 

## Feedback Reports · Rollback 

- **5 · Create build feedback reports** 

##### **6 · Capability to roll back** 

A clear picture of the whole build process 

Efficient deployment needs a way back 

File differences in this build 

Replace a defective release with a working one 

Defects addressed and features implemented Invaluable for tracebacks when things break 

This is where build and repository labels pay off If you cannot roll back, you cannot deploy boldly 

**Rollback is what makes frequent deployment safe rather than reckless.** 

27 

CI/CD with GitLab 

Pipelines, .gitlab-ci.yml and runners — the hands-on half 

28 

## Why CI/CD? 

It encourages collaboration across every department — and delivers these specific benefits. 

**01** 

**CI detects errors quickly** 

Fix them while they are still fresh in your mind 

**02** 

**CI reduces integration problems** 

Smaller problems are easier to digest and don't compound 

**03** 

**CI lets teams develop faster** 

More confidence means less bottlenecking 

**04** 

**CD ensures every change is releasable** 

Lowers the risk of each release — releases become boring 

**05** 

**CD delivers value more often** 

Fast feedback on what your end users actually care about 

**Three of the five benefits come from CI alone — before you automate a single deployment.** 

29 

## GitLab's Recommended Process 

One tool spanning the whole DevOps lifecycle. 



<!-- Start of picture text -->
Manage Plan Create Verify Package Secure Release Configure Monitor Protect<br>CI/CD lives here<br>1 2 3 4 5<br>Create MR Push code Collaborate Approval Merge & release<br>from an issue build & test runs review & fix on a review app then deploy<br><!-- End of picture text -->

30 

## How GitLab CI/CD Works 

Five steps, every time you push. 

> **1 You set up one or more runners on suitable hosts** 

> **2 You commit a .gitlab-ci.yml file to the repository** 

> **3 GitLab triggers the pipeline and schedules the jobs** 

> **4 Jobs are sent out to the runners** 

> **5 Runners send the results back to GitLab** 

31 

## Jobs, Stages & Runners 

Three words that explain every GitLab pipeline. 

**Job Stage Runner** WHAT you want to WHEN and how jobs run. WHO does the work. A accomplish. A job is Tests run in a stage after the lightweight agent that executed by a runner. one that compiles. executes the job. **`build test deploy`** `build-code unit-tests deploy-prod build-docs lint` **jobs in a stage run in parallel   ·   stages run in order** 

32 

## How a Pipeline Progresses 

**All jobs in a stage succeed** _the happy path_ Every job in the stage runs in parallel They all come back green The pipeline moves on to the next stage 

**One job in a stage fails** _the pipeline stops_ The failing job is reported immediately The next stage is not (usually) executed You fix it and push again 



<!-- Start of picture text -->
build test review deploy<br>—<br>✓ ✓ ✕<br>review failed, so deploy never runs<br><!-- End of picture text -->

33 

## Ways to Trigger a Pipeline 

Push to the GitLab repository — by far the most **Push code** ★ common **Run manually** Start it yourself from the GitLab UI **Schedule it** Set it to run at a later time, or on a cron schedule **Upstream pipeline** Triggered by another pipeline finishing Launch a pipeline programmatically with a trigger **The API** token 

★ **This is the one we shall use in the exercise.** 

34 

## .gitlab-ci.yml 

The whole pipeline is one YAML file in the root of your repository. 

```
stages:
```

```
-build
-deploy
variables:
```

```
KUBE_DOMAIN:example.com
```

**Lives in the repo root** Version-controlled like any other file 

**Defines stages** 

The order work happens in 

```
build:
```

```
stage:build
script:
```

```
-command build
```

**Defines jobs** Each with a stage and a script 

```
deploy:
```

```
stage:deploy
script:
```

```
-command deploy
```

**Reviewed like code** Pipeline changes go through merge requests too 

**Full keyword reference: docs.gitlab.com/ci/yaml/** 

35 

## Stages 

##### Stages separate jobs into logical sections. Jobs do the actual work. 

### **Build** 

Source code and dependencies are combined and built 

### **Test** 

Automated tests run to validate the code and its behaviour 

### **Review** 

The code goes through review apps for peer review and approval 

### **Deploy** 

The final product is deployed to a designated environment 

```
stages:
```

- `build` 

- `- test` 

- `review` 

- `deploy` 

_These four are the defaults — you can define any stages you like, and any number of jobs per stage._ 

36 

## Jobs & Scripts 

**Each stage can have many jobs** Give each one a name and a stage **Jobs in a stage run in parallel** So keep them independent of each other **script can be written several ways** One command, a list, or a shell script 

```
build-code:
stage:build
script:build-it.sh
build-other-code:
stage:build
script:src/other/build.sh
```

##### **Three ways to write script** 

```
script:command build
```



<!-- Start of picture text -->
script:<br>- npm install<br>- npm build<br><!-- End of picture text -->

```
script:
-scripts/build.sh
```

37 

## image & services 

What your job runs inside, and what it runs alongside. 

##### **`image`** 

The Docker image the job executes in. Pulled from Docker Hub by default, or from the GitLab Container Registry. 

##### **`services`** 

Tells the runner that additional images are needed alongside your job — a database, for example. 

```
a public image
image:ruby:2.3
```

```
services:
```

```
-postgres
```

```
a custom image
```

```
image:registry.gitlab.com/
gitlab-org/sample:latest
```

Your job container and the service containers share a network — the database is just there. 

```
our .gitlab-ci.yml so far
```

```
image:registry.example.com/k8-deploy:latest
services:
-postgres
```

38 

## variables 

Values your jobs can read — configuration, not secrets in the file. 

```
variables:
```

```
POSTGRES_DB:rails-sample_test
POSTGRES_USER:root
POSTGRES_PASSWORD:"xyzzy"
```

**Defined in the file** 

Fine for non-sensitive configuration 

**Or in project settings** Settings > CI/CD > Variables — use this for secrets **Available to every job** Referenced as $NAME inside your scripts 

**Never put real passwords or tokens in .gitlab-ci.yml — it is committed to the repository. Use Settings > CI/CD > Variables, and mask them.** 

39 

## cache & artifacts 

Two ways to carry files between jobs — for different reasons. 

#### **cache** 

#### **artifacts** 

_for dependencies you re-download_ 

_for output you want to keep_ 

Passes information between jobs and stages Typically node_modules, gems, pip packages A speed optimisation — safe to lose 

Build output you want to save or download Passed to later stages, and browsable in the UI Can be kept only when the job succeeds 

```
cache:
paths:
-binary/
-.config
```

```
artifacts:
when:on_success
paths:
-bin/target
```

_Rule of thumb: if losing the file only costs you time, cache it. If losing it costs you the build output, make it an artifact._ 

40 

## environment & when: manual 

Where the app is deployed — and who presses the button. **`environment`** 

#### **`when: manual`** 

Defines where the app is deployed. Three parts: a name, a URL, and when it runs. 

```
environment:
name:prod
url:
http://$CI_PROJECT_NAME.$KUBE_D
OMAIN
```

Holds the job until a human starts it from the UI. This is exactly what separates Continuous Delivery from Continuous Deployment. 

```
deploy-prod:
stage:deploy
when:manual
```

_GitLab then tracks what is deployed where, and gives you a one-click rollback._ 

**Use it for anything that touches production.** 

```
putting them together
deploy-code:
stage:deploy
environment:
```

```
name:production
```

```
when:manual
```

41 

## Controlling When Jobs Run 

only / except is the old way. rules is the modern one. 

###### **`only / except`** 

###### **`rules`** 

```
pseudo-deploy:
stage:deploy
script:
-command deploy_review
only:
-branches
except:
-main
```

```
pseudo-deploy:
stage:deploy
script:
-command deploy_review
rules:
```

- `if: '$CI_COMMIT_REF_NAME == "main"'` **`when:`** `never` 

- `- when: always` 

only = branches to run on.   except = branches to skip. 

Conditions on any variable, with full control over when. 

**rules is an improved, more powerful replacement for only/except. Prefer it in new pipelines — GitLab recommends it.** 

42 

## before_script & after_script 

Setup and teardown that wrap every job. 

##### **before_script** 

_runs before the job's own script_ 

Runs in every job, including deploy jobs 

Runs after artifacts are restored Used to install dependencies or update the image 

###### **`before_script:`** 

- `echo $CI_BUILD_STAGE` 

##### **after_script** 

_runs after the job — even failed ones_ 

Runs whether the job passed or failed 

Used for cleanup and collecting logs 

Runs inside the job and can interact with it 

###### **`after_script:`** 

   - `rm temp/*.tmp` 

- `apt-get update` 

- `bundle install` 

- `npm install` 

43 

## tags 

How a job chooses which runner picks it up. 

**Selects a runner Not Git tags More is fine** Tags match a job to runners CI tags and Git tags are A runner with extra tags can that can handle it entirely different things still run the job 



<!-- Start of picture text -->
job-name:<br>tags:<br>- ruby<br>- test<br><!-- End of picture text -->

**A job with no tags at all can be picked up by any runner.** 

44 

## The Complete .gitlab-ci.yml 

Everything from the last ten slides, in one file. 

```
image:registry.example.com/k8-
deploy:latest
services:
```

```
-postgres
```

```
variables:
POSTGRES_DB:rails-sample_test
cache:
```

```
paths:
```

- `binary/` 

```
stages:
```

- `build` 

- `test` 

- `deploy` 

```
build-it:
stage:build
script:
```

- `command build` 

- **`only:`** 

- `main` 

- **`tags:`** 

   - `osx` 

```
artifacts:
```

```
when:on_success
paths:
```

- `bin/target` 

```
deploy-code:
stage:deploy
script:
```

- `command deploy` 

```
when:manual
```

45 

## GitLab Runners 

The lightweight agent that actually runs your CI/CD jobs. 

_"run build, then test"_ 

**`.gitlab-ci.yml`** instructions, in the repo root 

**GitLab Runner** the agent that executes them 

**Runs anywhere** Linux, macOS, Windows, FreeBSD, cloud, bare metal, Docker 

**Any language** .NET, Java, Python, C, PHP — it just runs your commands **Anywhere you can build a Go binary, you can run a GitLab Runner.** 

**Created by an admin** Registered against the instance, a group, or a project 

46 

## A Runner Can Be… 

Three independent choices, made when the runner is registered. 

**Shared or Specific** 

**Shared** 

Available to every project with similar requirements. Managed by the GitLab admin, usually auto-scaling. **_vs_** 

**Specific** Tied to one or more particular projects. Managed by the runner owner — for specialised builds or billing. 

**Tagged or Untagged** 

**Tagged** Only runs jobs carrying the same tag. **_vs_** 

**Untagged** Only runs jobs that have no tags at all. 

##### **Protected or Not** 

**Protected** 

Only runs jobs from protected branches and protected tags. Use for runners holding deploy keys. **_vs_** 

**Not protected** 

Runs jobs from any branch. Fine for ordinary builds. 

47 

## Executors 

##### How the runner actually executes your job. 

##### **Common** 

**Docker** ★ Executes inside a Docker image. The most common by far. 

**Shell** 

Runs commands directly, as if typed into a terminal. 

**Docker Machine** 

A main machine scales runners up on demand. Typical in the cloud. 

**Kubernetes** Runs as a pod in a K8s cluster. Can also autoscale. 

**Less common** 

**VirtualBox** A base VM; the main machine clones it per runner. 

**Parallels** Same idea, on the Parallels platform. ★ **Use the Docker executor unless you have a specific reason not to.** 

**SSH** Like shell, but fewer features — no caching, bash only. 

48 

## Recap & Exercise 

**What we covered** 

#### **Your exercise** 

✓ 

CI: integrate small changes, continuously 

> ✓ Add a .gitlab-ci.yml to your personal project 

> ✓ Build and test automation 

> ✓ Define some build and test stages 

Delivery vs deployment, and the 6 CD ✓ principles 

> ✓ Make the pipeline go green on a push 

> ✓ GitLab pipelines, YAML and runners 

> ✓ Add a manual deploy job – coming soon 

**New exercise – Next Week·   Keyword reference: docs.gitlab.com/ci/yaml/** 

49 

