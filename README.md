# ELKeychain [![Build Status](https://travis-ci.org/Electrode-iOS/ELKeychain.svg?branch=master)](https://travis-ci.org/Electrode-iOS/ELKeychain)

A Swift framework for storing, retrieving, and removing generic password items in the system Keychain.

## Installation

### Carthage

Install with [Carthage](https://github.com/Carthage/Carthage) by adding the framework to your project's [Cartfile](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#cartfile).

```
github "Electrode-iOS/ELKeychain" ~> 0.0.1
```

### Manual

Install manually by adding `ELKeychain.xcodeproj` to your project and configuring your target to link `ELKeychain.framework`.

## Usage

### Storing a Generic Password Item

```
let password = "12345"

do {
  try Keychain.set(password, account: "king-roland", service: "druidia-airshield")
} catch let error {
    // failed to store keychain item
}

```

### Retrieving a Generic Password Item

```
do {
    if let password: String = try Keychain.get(account: "king-roland", service: "druidia-airshield") {
        Airshield.unlock(password: password)
    } else {
      // unable to find password to unlock
    }

} catch let error {
    // an error occurred while retrieving the keychain item
}


```

### Removing a Generic Password Item

```
do {
    try Keychain.delete(account: "king-roland", service: "druidia-airshield")
} catch let error {
    // an error occurred while trying to delete the keychain item
}

```

### Storing a Generic Password Item w/ Access Control

```
do {
    let accessControl = try AccessControl(protection: .whenPasscodeSetThisDeviceOnly, policy: .UserPresence)
    try Credential.keychain.set("12345", account: "king-roland", accessControl: accessControl)
} catch let error {
    // an error occurred
}

```
