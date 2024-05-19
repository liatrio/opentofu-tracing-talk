---
theme: slidev-theme-liatrio
author: blairdrummond
download: true
mdc: true
layout: cover-with-image
image: /Logos.svg
backgroundSize: contain
---

# Tracing Terraform Modules 

### Enabling Product Thinking with OpenTelemetry (and OpenTofu)

Blair Drummond

---
layout: image-right
image: /ca-tf-modules.png
backgroundSize: 30em 90%
---

# Reusable Terraform Modules

Common pattern in enterprises. Teams can leverage platform-provided terraform modules.

### Architecture Patterns

- Platform teams can provide "best practice" designs/baselines

### Security Guardrails built in

- Regulated environments can re-use secure-by-default modules

---

# We asked: How do we measure success?

<Transform :scale="1.1">

### Are your modules being used?

- Which teams are using your modules? Which versions?
- *How often are the modules run?*

### What is the developer experience of your modules?

- How fast do they deploy?
- If there are errors, what are the errors?


### Are errors reported manually or automatically?

- Are users reporting the errors to the platform team?
</Transform>

---

# Deja-Vu: We've done this before

<Transform :scale="1.7">

### This is just Observability

- *traces:* see speed, errors, and dependencies

- *metrics:* capture usage statistics

- *understand* how people use our service

- *investigate* unexplained errors

</Transform>

---
layout: image-right
image: /trace-with-errors.png
backgroundSize: 30em 70%
---

# What could "Good" Look like? 

- Instrument CI/CD Pipelines and or the [Flux Tofu-Controller](https://github.com/flux-iac/tofu-controller)
- Instrument [OpenTofu](https://opentofu.org/) 
- We can now observe infrastructure management!

### This would be a boring talk if we didn't share the code

- [github.com/liatrio/opentofu-tracing-talk](https://github.com/liatrio/opentofu-tracing-talk)

- This is a PoC, but this aligns with ongoing efforts in the OTel community

---

<Transform :scale="1.2">

# Why this is awesome

- Existing terraform modules require no changes.
- Recursively traces all sub-modules
- Gets all module version info, *even for unpinned modules*. 
- External API calls can be traced too 🤯

### Tracing FTW

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

### Where is the value?

- Which modules are widely used? Prioritize!

### Version adoption curves

- Who's on old versions of a module?

### Drift-Detection

- Modules which change resources every run may be non-idempotent!

---

# What's next?

### Environment Variable Context Propogation

- Shockingly, context propogation for non-HTTP interactions **does not exist**
- We used an *informal but common* convention called `TRACEPARENT`.
- Support for environment variable propogation is in-progress:
  + [opentelemetry-specification issue #740](https://github.com/open-telemetry/opentelemetry-specification/issues/740)
  + [opentelemetry proposal PR #241](https://github.com/open-telemetry/oteps/pull/241)
  
### CI/CD Semantic Conventions
  
- We're in the OTel Semantic Conventions SIG working on CI/CD schema standards
  + [open-telemetry/semantic-conventions issue #915](https://github.com/open-telemetry/semantic-conventions/issues/915)
  
- This will make Tofu-Controller generated traces interoperable and standardized

---

# What's next? (Part 2)

<Transform :scale="1.8">

### Tracing isn't just for Web Services

- OTel for CI/CD and Batch is going to be a game-changer.
- *This technology will all feel obvious in retrospect.*

### Just Adopt OTel

</Transform>

---
layout: two-cols
---

<style>
.col-right .h3 {
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

# The ` ` Liatrio` `Team

<Transform :scale="1.6">

### Collaborators:

Thanks to my collaborators on this project

- Ryan Hoofard
- Alice Jones
- Adriel Perkins

who are the reason there's code here!

</Transform>

::right::

<Transform :scale="1.7">

### Speaker

![me](/me.jpg){width=100%}

Blair Drummond

[blaird@liatrio.com](mailto:blaird@liatrio.com)

</Transform>

---
layout: about
---

---
layout: mic-drop
---
