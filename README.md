# Practical Computer Security

This repository documents practical security exercises covering common
vulnerabilities, defensive techniques, and security tooling. The notes focus on
the reasoning behind each experiment, the relevant commands, and the observed
results.

## Topics

- Environment variables and set-user-ID security
- Buffer overflows and format-string vulnerabilities
- Cross-site scripting (XSS) and request forgery
- Hash length-extension attacks
- Symmetric encryption modes
- Public Key Infrastructure (PKI), certificates, and TLS
- Remote code execution vulnerabilities

## Repository structure

Each `LOGBOOK*.md` file contains the notes for one security topic. Supporting
screenshots are kept in the [`docs/`](docs/)
directory and are referenced from the corresponding notes.

## Usage

The notes are intended for learning and review. Commands and demonstrations
may require a Linux environment, Docker, OpenSSL, a debugger, or an isolated
test application. Do not run exploit demonstrations against systems you do not
own or have explicit permission to test.

Examples that depend on a particular lab environment use placeholders for
credentials, tokens, addresses, and other environment-specific values. Replace
them only with disposable values in an authorised, isolated setup.

## Credits

The original technical work and supporting material are preserved in the
individual logbooks. References to external projects and sources are retained
where relevant.

## License

No separate license has been specified for this repository. Contact the
repository owner before reusing the material beyond personal study.
