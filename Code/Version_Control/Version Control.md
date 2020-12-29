# Version Control

Version control should always be used and there are some conventions to standardize this labor.

## Version Control Itself

The code always have to be under version control, for this use [git](https://git-scm.com/)

> [Git Cheetsheet](#fixme)

## Version Numbers

### Overview

[version numbers](https://semver.org/) is a semantic way for taggin each version of the software, it's have a basic structure like this `X.Y.Z` where:

| Label | Meaning                                                                   |
| ----- | ------------------------------------------------------------------------- |
| X     | Mayor versión, when you make incompatible API Changes                     |
| Y     | Minor version, when you add functionality in a backward compatible manner |
| Z     | Patch versión, when you make backwards compatible bug fixes               |

Some people use 4 numbers like `X.Y.Z.B` where the `B` means _"Build Version"_ and increment it with each git commit.

### Rules

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

1. [](https://semver.org/#spec-item-1)

    Software using Semantic Versioning MUST declare a public API. This API could be declared in the code itself or exist strictly in documentation. However it is done, it SHOULD be precise and comprehensive.

2. [](https://semver.org/#spec-item-2)

    A normal version number MUST take the form X.Y.Z where X, Y, and Z are non-negative integers, and MUST NOT contain leading zeroes. X is the major version, Y is the minor version, and Z is the patch version. Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

3. [](https://semver.org/#spec-item-3)

    Once a versioned package has been released, the contents of that version MUST NOT be modified. Any modifications MUST be released as a new version.

4. [](https://semver.org/#spec-item-4)

    Major version zero (0.y.z) is for initial development. Anything MAY change at any time. The public API SHOULD NOT be considered stable.

5. [](https://semver.org/#spec-item-5)

    Version 1.0.0 defines the public API. The way in which the version number is incremented after this release is dependent on this public API and how it changes.

6. [](https://semver.org/#spec-item-6)

    Patch version Z (x.y.Z | x > 0) MUST be incremented if only backwards compatible bug fixes are introduced. A bug fix is defined as an internal change that fixes incorrect behavior.

7. [](https://semver.org/#spec-item-7)

    Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards compatible functionality is introduced to the public API. It MUST be incremented if any public API functionality is marked as deprecated. It MAY be incremented if substantial new functionality or improvements are introduced within the private code. It MAY include patch level changes. Patch version MUST be reset to 0 when minor version is incremented.

8. [](https://semver.org/#spec-item-8)

    Major version X (X.y.z | X > 0) MUST be incremented if any backwards incompatible changes are introduced to the public API. It MAY also include minor and patch level changes. Patch and minor version MUST be reset to 0 when major version is incremented.

9. [](https://semver.org/#spec-item-9)

    A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST NOT include leading zeroes. Pre-release versions have a lower precedence than the associated normal version. A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92, 1.0.0-x-y-z.--.

10. [](https://semver.org/#spec-item-10)

    Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85, 1.0.0+21AF26D3----117B344092BD.

11. [](https://semver.org/#spec-item-11)

    Precedence refers to how versions are compared to each other when ordered.

    1. Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence).

    2. Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.

        Example: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1.

    3. When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:

        Example: 1.0.0-alpha < 1.0.0.

    4. Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows:

        1. Identifiers consisting of only digits are compared numerically.

        2. Identifiers with letters or hyphens are compared lexically in ASCII sort order.

        3. Numeric identifiers always have lower precedence than non-numeric identifiers.

        4. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.

        Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

## Change Log

### Overview

A [change log](https://keepachangelog.com/en/0.3.0/) is the description of the **notable** changes between versions.

### Rules

- It's made for humans, not machines, so legibility is crucial.
- Easy to link to any section (hence Markdown over plain text).
- One sub-section per version.
- List releases in reverse-chronological order (newest on top).
- Write all dates in `YYYY-MM-DD` format. (Example: `2012-06-02` for `June 2nd, 2012`.) It's international, [sensible](https://xkcd.com/1179/), and language-independent.
- Explicitly mention whether the project follows [Semantic Versioning](https://semver.org/).
- Each version should:
  - List its release date in the above format.
  - Group changes to describe their impact on the project, as follows:
  - `Added` for new features.
  - `Changed` for changes in existing functionality.
  - `Deprecated` for once-stable features removed in upcoming releases.
  - `Removed` for deprecated features removed in this release.
  - `Fixed` for any bug fixes.
  - `Security` to invite users to upgrade in case of vulnerabilities.

### [Example](https://github.com/olivierlacan/keep-a-changelog/blob/master/CHANGELOG.md)