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
layout: two-cols
---

![OpenTelemetry](/otel.png){width=280}

- The standard supported by all major log/metric/tracing providers
- OpenTelemetry enables *distributed tracing* and *context propogation*

::right::

<div class="mt-14"></div>

![OpenTofu](/opentofu.svg){width=200}

- The open source fork of Terraform (Linux Foundation)


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
- Recursively traces all sub-modules
- Gets all module version info, *even for unpinned modules*. 
- External API calls can be traced too 🤯

</Transform>

---

# `TRACEPARENT`

<Transform :scale="0.8">

```go
	var ctx context.Context
	var otelSpan trace.Span
	var displayArgs string
	{
		// At minimum we emit a span covering the entire command execution.
		_, displayArgs = shquot.POSIXShellSplit(os.Args)
		if os.Getenv("TRACEPARENT") != "" {
			tp, _ := traceparent.LoadFromEnv()
			var flags trace.TraceFlags = 0
			if tp.Sampling {
				flags = 1
			}
			sc := trace.SpanContext{}.
				WithTraceID(trace.TraceID(tp.TraceId)).
				WithSpanID(trace.SpanID(tp.SpanId)).
				WithTraceFlags(flags).
				WithRemote(true)
			ctx, otelSpan = tracer.Start(trace.ContextWithRemoteSpanContext(context.Background(), sc), fmt.Sprintf("tofu %s", displayArgs))

		} else {
			ctx, otelSpan = tracer.Start(context.Background(), fmt.Sprintf("tofu %s", displayArgs))
		}
		defer otelSpan.End()
	}
```

</Transform>

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
image: /span-metrics.png
backgroundSize: 30em 60%
---

# Deriving metrics

- Which modules are widely used? Prioritize!

- Are people upgrading their Terraform modules?

- Drift-Detection: Modules which change resources every run may be non-idempotent!

---
layout: image
image: /module-usage.png
backgroundSize: 100%
---

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


<div class="slidev-layout flex">
  <div class="item flex">
    <Portrait src="/ryan.png" name="Ryan Hoofard" title="DevOps Engineer" />
  </div>
  <div class="item flex">
    <Portrait src="/alice.png" name="Alice Jones" title="Lead DevOps Engineer" />
  </div>
  <div class="item flex">
    <Portrait src="/adriel.png" name="Adriel Perkins" title="Lead DevOps Engineer" desc="OTel member" />
  </div>
</div>


---
layout: two-cols
---

# Thanks for Listening!

<Transform :scale="1.3">

<div class="slidev-layout flex -mt-30 -ml-20">
<FramelessPortrait src="/me.png" name="Blair Drummond" title="Lead DevOps Engineer" desc="Kubernetes nerd (Montréal)" email="blaird@liatrio.com"/>
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
    <QRCode value="https://liatrio.com" />
  </div>
  <div class="h-8 mt-7 ml-5">
    <h2>liatrio.com</h2>
  </div>
</div>
  
