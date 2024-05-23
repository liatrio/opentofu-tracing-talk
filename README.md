# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `npm install`
- `npm run dev`
- visit http://localhost:3030

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev on [documentations](https://sli.dev/).


# Demo

To be able to see some of awesomeness of what we can do with an instrumented tofu-controller and opentofu binary, navigate to our [quickstart repo](https://github.com/liatrio/tag-o11y-quick-start-manifests/tree/updating-traces-overlay) and follow the instructions for how to deploy the `traces` configuration.  You need to have a local cluster running to be able to deploy the configuration and once its up and running, you can port-forward `Grafana` to be able to see the tracing in action with our own custom dashboard.  

### Tofu Controller

One of the two core components that enables this tracing is the [Tofu Controller](https://flux-iac.github.io/tofu-controller/).  We have our own fork with the changes we made to enable this tracing which can be found [here](https://github.com/liatrio/tofu-controller/tree/tracing)

### OpenTofu

The other core component that enables this tracing is [OpenTofu](https://opentofu.org).  Like before, we also have our own version with the changes we made to enable this tracing which can be found [here](https://github.com/liatrio/opentofu/tree/tracing)
