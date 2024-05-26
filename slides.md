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

# Tracing Terraform Modules 

### Enabling Product Thinking with OpenTelemetry (and OpenTofu)

Blair Drummond

---

![OpenTofu](/opentofu.svg){width=400px}

<Transform :scale="1.8">

- The Open Source Successor to Terraform

- Also `Weave TF-Controller => Flux Tofu-Controller`

</Transform>

---

# A Trace is like Poutine

![Traces Explained](/trace-explained2.png)

---
layout: image-right
image: /ca-tf-modules.png
backgroundSize: 30em 90%
---

# Reusable Terraform Modules

<Transform :scale="1.7">

- Security Guardrails built-in

- Quick-Start for app teams

</Transform>

---

# How do we measure success?

<Transform :scale="1.8">

- Are your modules being used? Which ones?

- Are errors reported manually or automatically?

</Transform>

---

# ...This is just Observability

<Transform :scale="2.1">

- *traces:* see speed, errors, and dependencies

- *metrics:* capture usage statistics

</Transform>

---

# What could "Good" Look like? 

<Transform :scale="1.8">

- Trace the modules used (recursively)

- Understand which teams are calling these modules

- Correlate errors to the modules and teams impacted

</Transform>

---

# Insight requires instrumentation end-to-end

<Transform :scale="1.8">

- Instrument [OpenTofu](https://opentofu.org/) 

- Instrument the Orchestator:
  + in this case, the [Flux Tofu-Controller](https://github.com/flux-iac/tofu-controller)

</Transform>

---

## Tofu-Controller (Flux) orchestrates `tofu plan/apply`

![tofu-controller](/tf-controller-basic-architecture.png){width=800}

---
layout: image-right
image: /trace-with-errors.png
backgroundSize: 30em 70%
---

<div class="mb-20"></div>

### This would be a boring talk if we didn't have code

- [github.com/liatrio/tag-o11y-quick-start-manifests](tag-o11y-quick-start-manifests)

<div class="ml-30 mt-5">
<QRCode value="https://github.com/liatrio/tag-o11y-quick-start-manifests" />
</div>

- *This is a PoC, but this aligns with ongoing efforts in the OTel community*

---
layout: image
image: /detailed-trace.png
backgroundSize: 100%
---

---

# Why this is awesome

<Transform :scale="1.7">

- Existing terraform modules require no changes.

- Gets all submodule version info, *even for unpinned modules*. 

</Transform>

---

# Deriving metrics

<Transform :scale="1.7">

- Which modules are widely used? Prioritize!

- Are people upgrading their Terraform modules?

- Drift-Detection: important to catch!

</Transform>

---
layout: image
image: /module-usage.png
backgroundSize: 100%
---

---

<Transform :scale="1.7">

# Moving Upstream

- The stuff we did isn't spec compliant, yet...

- ...Because we're working upstream on the spec

</Transform>

---
layout: image
image: /ci-cd-conventions.png
backgroundSize: 90%
---

---
  
# CI/CD Observability end-to-end
  
<div class="grid grid-cols-2 mt-12 ml-10 w-250">
  <div class="h-48 mt-15">
    <p class="flex -ml-11" style="width: 220px; text-align: center;">Liatrio's Grafana Dashboard</p>
    <QRCode value="https://grafana.com/grafana/dashboards/20976-engineering-effectiveness-metrics/" size=130 />
  </div>
  <div class="h-480 -ml-70 -mt-10">

![Git Metrics](/grafana.drawio.png){width=600}

  </div>
</div>

---

# Takeaways

<Transform :scale="1.7">

### Tracing isn't just for Web Services

- OTel for CI/CD and Batch is going to be a game-changer.
- *This technology will all feel obvious in retrospect.*

</Transform>

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
  
