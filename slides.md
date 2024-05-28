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

- Security Guardrails built-in

- Reduce cognitive load

</Transform>

---
layout: image-right
image: /you-dont.jpg
backgroundSize: 30em 90%
---

# Platform Teams today

<div class="mt-20"></div>

### Which versions of your modules are being used?

<Transform :scale="3.8">🤷‍♀️</Transform>

---

<Transform :scale="1.4">

### How are errors reported and handled?

<Transform :scale="1.4">... tickets from frustrated developers?</Transform>

<div class="mt-20"></div>

### How do we prioritize improvements?

<Transform :scale="1.4">... </Transform>

</Transform>


---

# Making it Observable

<Transform :scale="1.8">

- Trace the modules used (recursively)

- Correlate errors to the modules and teams impacted

</Transform>

---

# Instrumenting OpenTofu

<Transform :scale="1.8">

- We instrumented OpenTofu to try this out!

- But, `tofu init` and `tofu apply` couldn't share context

</Transform>

---

# Tofu-Controller to join `init` and `apply`

<Transform :scale="1.8">

- Opted to instrument the [Flux Tofu-Controller](https://github.com/flux-iac/tofu-controller)

- (CI/CD pipeline could also work)

</Transform>

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

# Food for thought 

<div class="mt-30"></div>

<Transform :scale="1.8">

### How could Tracing improve your CI/CD?

</Transform>

---

# OpenTelemetry for CI/CD: work in progress

<Transform :scale="1.7">

- Work ongoing on common standards for this

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

<Transform :scale="1">

<div class="grid grid-cols-2 mt-0 ml-30 w-200 h-400">
  <div class="slidev-layout flex w-80 h-10">
    <Portrait src="/ryan.png" name="Ryan Hoofard" title="DevOps Engineer" />
  </div>
  <div class="slidev-layout flex -ml-20 -mt-1 w-85 h-10">
    <Portrait src="/alice.png" name="Alice Jones" title="Lead DevOps Engineer" />
  </div>
</div>

</Transform>

- Test

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
  
