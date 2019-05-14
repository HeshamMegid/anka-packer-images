Packer scripts for use with Veertu Anka
=======================================

This provides a basic MacOS + Xcode for automated testing of macOS/iOS.

This script requires Veertu Anka installed and [our packer builder](https://github.com/buildkite/packer-builder-veertu-anka).

There are two stages of images, which can be thought of like layers. This allows
for reasonably rapid iteration on the scripts, as working stages can be re-used.

Get Started
-----------

Checkout this repository to a directory:

```bash
git clone git@github.com:buildkite/anka-packer-images.git
cd anka-packer-images/
make macos-10.12
make macos-xcode-10.12 source_vm=macos-base-10.12-r1
```

Phase 1: Basic macOS
--------------------

The base layer is essentially macOS as the Veertu Anka leaves it post-install, with
the following things added:

- Homebrew
- Xode Developer Tools
- rbenv and plugins
- Ruby 2.4.0

It builds images in the form: `macos-base-X.X-rX`

```bash
make macos-10.12
```

Phase 2: Xcode and Fastlane
---------------------------

The base layer is the slowest layer, as it downloads and installs Xcode. It contains
the following:

- Xcode (defaults to 8.3.3)
- Fastlane
- Carthage
- Swiftlint
- CocoaPods

It builds images in the form: `macos-X.X-xcode-X.X.X-rX`.

```bash
make macos-10.12-xcode xcode_version=8.3.3 source_vm={image_name_from_previous_step}
```
