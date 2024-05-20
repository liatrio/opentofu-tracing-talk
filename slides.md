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
  font-family: "Verdana";
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

.col-right h3 {
  width: 50%;
  margin: 0 auto;
  text-align: center ;
}

.col-right img {
  width: 50%;
  display: block;
  margin: 0 auto;
  text-align: center ;
}

.col-right {
  width: 50%;
  margin: 0 auto;
  text-align: center ;
}
</style>

# Tracing Terraform Modules 

### Enabling Product Thinking with OpenTelemetry (and OpenTofu)

Blair Drummond

---


TODO explain what OpenTofu and OpenTelemetry are?

---
layout: image-right
image: /ca-tf-modules.png
backgroundSize: 30em 90%
---

# Reusable Terraform Modules

<Transform :scale="1.7">

- Security Guardrails built-in

- Quick-Start for app teams

- Standard Architectures

</Transform>

---

# We asked: How do we measure success?

<Transform :scale="1.8">

- Are your modules being used? Which ones?

- What is the developer experience of your modules?

- Are errors reported manually or automatically?

</Transform>

---

# ...This is just Observability

<Transform :scale="1.8">

- *traces:* see speed, errors, and dependencies

- *metrics:* capture usage statistics

- *investigate* unexplained errors

</Transform>

---


# What could "Good" Look like? 

<Transform :scale="1.8">

- Instrument [OpenTofu](https://opentofu.org/) 
- Instrument CI/CD and/or the [Flux Tofu-Controller](https://github.com/flux-iac/tofu-controller)
- Enrich telemetry with attributes from git/kubernetes

</Transform>

---
layout: image-right
image: /trace-with-errors.png
backgroundSize: 30em 70%
---

### This would be a boring talk if we didn't have code

- [github.com/liatrio/opentofu-tracing-talk](https://github.com/liatrio/opentofu-tracing-talk)

- *This is a PoC, but this aligns with ongoing efforts in the OTel community*

---

todo fullscreen shot of the trace to show transitive module errors

---

# Why this is awesome

<Transform :scale="1.7">

- Existing terraform modules require no changes.
- Recursively traces all sub-modules
- Gets all module version info, *even for unpinned modules*. 
- External API calls can be traced too 🤯

</Transform>

---

TODO code-snippet that shows TRACEPARENT and tracing apply

---

<Transform :scale="1.8">

### *Tracing FTW*

- When we see an error we'll know:
  + the resource in the module that caused the error 
  + which git commit the plan/apply was run against
  + which team encountered the issue

</Transform>

---
layout: image-right
image: /versions.png
backgroundSize: 30em 30%
---

# Deriving metrics

- Which modules are widely used? Prioritize!

- Are people upgrading their Terraform modules?

- Drift-Detection: Modules which change resources every run may be non-idempotent!

---

# What's next?

<Transform :scale="1.4">

### Environment Variable Context Propogation

- Context propogation for non-HTTP interactions **does not exist yet**
- We used an *informal but common* convention called `TRACEPARENT`
- Support for environment variable propogation is in-progress:
  + [opentelemetry-specification issue #740](https://github.com/open-telemetry/opentelemetry-specification/issues/740)
  + [opentelemetry proposal PR #241](https://github.com/open-telemetry/oteps/pull/241)

</Transform>
  
---
  
# What's next?

<Transform :scale="1.4">

### CI/CD Semantic Conventions
  
- We're in the OTel group for CI/CD Semantic Conventions
  + [open-telemetry/semantic-conventions issue #915](https://github.com/open-telemetry/semantic-conventions/issues/915)
  
- This will inform Pipeline/Tofu-Controller trace attributes

</Transform>

---

# What's next? (takeaways)

<Transform :scale="1.4">

### Tracing isn't just for Web Services

- OTel for CI/CD and Batch is going to be a game-changer.
- *This technology will all feel obvious in retrospect.*

</Transform>

---

# Collaborators

<div style="font-size: 30px;">
Thanks to my Liatrio colleagues, who implemented a lot of this work and without whom there would not have been a demo!
</div>


<div class="slidev-layout flex">
  <div class="item flex">
    <Portrait src="/ryan.png" name="Ryan Hoofard" title="DevOps Engineer" />
  </div>
  <div class="item flex">
    <Portrait src="/alice.png" name="Alice Jones" title="DevOps Engineer" />
  </div>
  <div class="item flex">
    <Portrait src="/adriel.png" name="Adriel Perkins" title="DevOps Engineer" />
  </div>
</div>


---
layout: two-cols
---

# Thanks!

<div class="slidev-layout flex -mt-5">
<Portrait src="/me.png" name="Blair Drummond" title="DevOps Engineer" desc="Kubernetes nerd (Montréal)" email="blaird@liatrio.com"/>
</div>

::right::

<img src="/liatrio.png" style="padding-top: 30px; padding-bottom: 50px; transform: scale(3);" />


TODO put cards with what Liatrio does here
