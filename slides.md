---
theme: slidev-theme-liatrio
author: blairdrummond
download: true
mdc: true
layout: cover-with-image
image: /Logos.svg
backgroundSize: contain
---

<style>
.slidev-layout.cover h1 {
   @apply text-3xl;
}

h1 {
  font-family: "DM Sans";
  text-transform: none;
}

h3 {
  font-weight: 800;
}

ul {
  padding-top: 20px;
}

ul ul {
  padding-top: 0px;
}
</style>

# Enabling Product Thinking for Terraform Modules

### with OpenTelemetry (and OpenTofu)

Blair Drummond

---

![TF Modules](/tf-modules.png){width=880px}

---
layout: image-right
image: /ca-tf-modules.png
backgroundSize: 30em 90%
---

# Reusable Terraform Modules

<Transform :scale="1.7">

- "Golden Path"

- Quick-Start for app teams

- Security Guardrails built-in

</Transform>

---

# How do we measure success?

<Transform :scale="1.8">

- Which versions of your modules are being used?

- Can we measure error rates?

</Transform>

---

# ...This is just Observability

<Transform :scale="2.1">

- *traces:* see speed, errors, and dependencies

- *metrics:* capture usage statistics

</Transform>

---

# Terraform modules as a Product

<Transform :scale="1.8">

- Trace the modules used (recursively)

- Understand which teams are calling these modules

- Correlate errors to the modules and teams impacted

</Transform>

---

# Instrumenting OpenTofu

<Transform :scale="1.8">

- We instrumented OpenTofu to try this out!

- But, `tofu init` and `tofu apply` couldn't share context

- Needed to instrument a layer up

</Transform>

---

# Tofu-Controller to join `init` and `apply`

<div class="grid grid-cols-2 mt-0 ml-27">

<div class="w-100 mt-20 -ml-30">

- Needed custom handling between `init` and `apply`

- Opted to instrument the [Flux Tofu-Controller](https://github.com/flux-iac/tofu-controller)

</div>


<div class="w-120 -ml-20">

### Jenkins did this first with the OTel plugin

![Jenkins](/jenkins.png)

</div>
</div>

---

# Trace of `tofu-controller` pipeline

![Trace](/trace-with-errors.png){width=750}

---

## The Who, What, Where of a Tofu Apply

<Transform :scale="1.9">

```yaml
# simplified Terraform resource
kind: Terraform
metadata:
  name: postgresql-rds        # <-- WHAT
  namespace: backstage-system # <-- WHO
spec:
  sourceRef: # <-- WHERE
    url: github.com/liatrio/rds-terraform-module
    ref:
      branch: main 
```

</Transform>

---

# Refesher on Traces

![Traces Explained](/trace-explained2.png)

---
layout: image
image: /detailed-trace.png
backgroundSize: 100%
---


---
layout: image
image: /module-usage.png
backgroundSize: 100%
---


---

# Try this out yourself! Everything on Github


<div class="grid grid-cols-2 mt-22 ml-27">

<div class="w-80 -ml-20">

<Transform :scale="1.8">

- Instrumented OpenTofu 
- Instrumented Tofu-Controller
- A demo Grafana Dashboard

</Transform>

</div>

<div class="ml-30 mt-10">
<QRCode size=150 value="https://github.com/liatrio/tag-o11y-quick-start-manifests" />

[liatrio/tag-o11y-quick-start-manifests](https://github.com/liatrio/tag-o11y-quick-start-manifests)

</div>

</div>


---

# Why this is awesome

<Transform :scale="1.7">

- Existing terraform modules require no changes.

- Gets all submodule version info, *even for unpinned modules*. 

</Transform>

---

# Takeaways

<div class="mt-30"></div>

<Transform :scale="1.8">

### CI/CD Tracing is the next frontier

- *We think this will feel obvious in retrospect.*

</Transform>

---

<Transform :scale="1.7">

# What's Next

- Jenkins led the way with their OTel plugin

- Other CI/CD engines (github, gitlab, etc) need to catch up

- Need CI/CD Semantic Conventions to unify approaches

</Transform>

---
layout: image
image: /ci-cd-conventions.png
backgroundSize: 90%
---

---

# Collaborators

<div style="font-size: 30px;">
Thanks to my Liatrio colleagues, who implemented a lot of this work and without whom there would not have been a demo!
</div>

<div class="slidev-layout flex -mt-10 ml-10 w-200">
  <div class="item flex">
    <Portrait src="/ryan.png" name="Ryan Hoofard" title="DevOps Engineer" />
  </div>
  <div class="item flex">
    <Portrait src="/alice.png" name="Alice Jones" title="Lead DevOps Engineer" />
  </div>
</div>


---
layout: two-cols
---

# Thanks for Listening!

<Transform :scale="1.3">

<div class="grid grid-cols-2 mt-30 ml-5 w-90">
  <div class="slidev-layout flex w-80 -mt-28 -ml-20">
    <FramelessPortrait src="/me.png" name="Blair Drummond" title="Principal DevOps Engineer" desc="Kubernetes nerd (Montréal)" email="blaird@liatrio.com"/>
  </div>
  <div class="slidev-layout flex w-80 -mt-28 -ml-20">
    <FramelessPortrait src="/adriel.png" name="Adriel Perkins" title="Lead DevOps Engineer" desc="Observability Practice Lead" email="adrielp@liatrio.com"/>
  </div>
</div>

</Transform>

::right::

<img src="/liatrio.png" class="w-50 ml-30" />

<div class="grid grid-cols-3 mt-10 w-80">
  <div class="h-48">
    <Icon icon="platforms" />    
    <Icon icon="security" />
  </div>
  <div class="h-48">
    <Icon icon="enablement" />   
    <Icon icon="cloud-native" /> 
  </div>
  <div class="h-48">
    <Icon icon="mlops" />        
    <Icon icon="modernization" />
  </div>
</div>
  
  
<div class="grid grid-cols-2 mt-12 ml-27 w-50">
  <div class="h-48">
    <QRCode value="https://hubs.ly/Q02yrGwg0" />
  </div>
  <div class="h-8 -mt-1 ml-5">
    <p class="text-l"><i>Observing Delivery Platforms.pdf</i></p>
  </div>
</div>
  
