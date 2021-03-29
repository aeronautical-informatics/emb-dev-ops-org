# Roadmap EmbDevOps

The target is to show a complete continous integration/continous development cycle (CI/CD) with the corresponding toolchain to support this approach.

![BDD cycle](bdd_cycle.png)

To show the capabilities of this approach and the technologies supporting it we want to present a small piece of avionics software created with this approach on the base of a formal specification used in real avionics equipment.

The following technologies will be used and explained in the project:

## Gherkin Tests
For the Test Driven Development (TDD) tests are the first stage of the process. To structure those tests the [Gherkin language](https://cucumber.io/docs/gherkin/reference/) is used. This is a formalisation on structured sentences with the goal of allowing automated evaluation for documentation or testing, while still providing an easy to read and understand format.

A Gherkin sentence is structured by certain keywoards that describe context (`GIVEN`), events (`WHEN`) and outcomes (`THEN`). Together these words can build sentences like:

`GIVEN the main windows is selected`

`WHEN the "Start"-button is pressed`

`THEN the window "Loading..." will appear`

`AND the window "Loading..." will be focussed.`

The bridge to go from this structured, but still natural and understandable language to code and tests will be created by a translation tool. But before we can use that we have to look at what kind of code we want to create.

## Rust
As a newer programming language with many by-design security features [Rust](https://www.rust-lang.org/) provides a very solid base for security critical applications that the avionics sector requires. For example memory-safety and thread-safety are guaranteed at compile-time by the rich type system and ownership model. 
With its good integrated package manager, detailed documentation and testing capabilities it is well equipped to be integrated into the CI/CD-cycle. 

## Testing
To translate the Gherkin sentences into usable tests we use the tool [Cucumber](https://cucumber.io/) or to be precise the language specific one for the Rust language ["cucumber-rust"](https://lib.rs/crates/cucumber_rust). This enables us to generate test examples and run these automatically and generate output like this, that tells us which tests succeded, which failed and which hasn't been implemented yet:

![Cucumber report](report-success-failure.png)

Together with these tests which can encompass bigger parts of the code base we will be using unit tests for smaller code fragments that are less complex. These will be created by the package manager of Rust [Cargo](https://doc.rust-lang.org/cargo/) with `cargo test`.

## Github/Gitlab actions
To automate and streamline the process further this testing approach will be used together in the GitHub flow. The well proven GitHub process of versioning, testing and releasing fits well with the overall CI/CD process. For the automation [GitHub actions](https://github.com/features/actions) will be used that run our Gherkin and unit tests on the pushed code automatically. 

## QEMU
In the last step the created program will be deployed to a simulated platform within [QEMU](https://www.qemu.org/) to find out if the tests still run successfully and if the version can be released. This step should be integrated into the Github actions script.