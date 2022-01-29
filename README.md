# Entity Compiler Standard Library

This repository defines a base set of domains, languages, units, etc. that can be used with most applications of the Entity Compiler. They attempt to be programming language agnostic and can help to provide some standardization at a basic level.

Your organization can decide to have their own standards or can participate in making this repository a standard in the industry so that templates can more easily be shared with those in the Entity Compiler community.

The repository contains the following directories:

| Directory | Description |
| ---------	| -----------	|
| [`domains`](domains) | Contains many standard domains that you can specialize in your applications. |
| [`ec`](ec) | The readme files in some of the directories are generated from its contents. This directory contains the configuration that runs the Entity Compiler to generate these readme files. |
| [`formatting`](formatting) | Contains file formatting definitions. |
| [`languages`](languages) | Contains many programming language definition files. As more and more people use the Entity Compiler for different programming languages, this can be expanded. |
| [`templates`](templates) | This is a collection of templates that are not specific to any framework, such as those that generate documentation or code around some kind of protocol. This would be a great place for contributors to add templates that are not specific to any particular framework. |
| [`units`](units) | Contains a file that attempts to standardize units for all users of the Entity Compiler. Contributions are welcome here as well to expand the supported units. |

## Licensing

All projects of the EntityC Organization are under the BSD 3-clause License.

See [LICENSE.md](LICENSE.md) for details.

## Contributing

Contributors are welcome. Before contributing please read the following [Contributing Guidelines](CONTRIBUTING.md).

## Code of Conduct

The Code of Conduct governs how we behave in public or in private whenever the project will be judged by our actions. We expect it to be honored by everyone who contributes to this project.

See [Code of Conduct](CODE_OF_CONDUCT.md) for details.
