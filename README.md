---
description: Here's the description of every role supported by Skydel.
---

# Roles

## SkydelCoreInterface

### Runtime Logging

During simulation initialization, Skydel will create a temporary folder for every plug-in instance. Existing folders will be wiped. Plug-in instances can access this path via the `setLogPath` method. The path have the following format: _Skydel Data Folder / Output / A / B_ where _A_ is the configuration name and _B_ the plug-in instance name.

### User Interface

When instantiating a plug-in, Skydel asks for a `QWidget*` via the `createUI` method. The returned widget will be displayed in Skydel user interface under _Settings / Plug-ins / B / Plug-in UI_ where _B_ is the plug-in instance name. Fully give the ownership of the widget pointer to Skydel, 

```cpp
QWidget* B::createUI()
{
    auto* ui = new QWidget{};
    
    // connect signal/slots
    
    return ui;
}
```

### Notification

When instantiating a plug-in, Skydel will create and give a `SkydelNotifierInterface*` to every plug-in instance via the `setNotifier` method. With this object, a plug-in instance can:

* Send 3 different type of notification to Skydel via the `notify` method
* Tell Skydel to change it's state to unsaved via the `setDirty` method

| `Type` | Description |
| :--- | :--- |
| `INFO` | \[Default\] Message logged in _simulator.log as_ an _info_ |
| `WARNING` | Message logged in _simulator.log_ and Skydel _Status Log_ tab as a _warning_ |
| `ERROR` | Message logged in _simulator.log and_ Skydel _Status Log_ tab as an _error_ |

Sending an `ERROR` notification at runtime will cause the simulation to stop.

```cpp
void B::setNotifier(SkydelNotifierInterface* notifier)
{
    // Sends an warning message to Skydel
    notifier->notify("Hello", SkydelNotifierInterface::Type::WARNING);
    
    // Tells Skydel to change it' state to unsaved
    notifier->setDirty();
}
```

### Configuration

When saving, Skydel will demand a `QJsonObject` for every plug-in instance via the `getConfiguration` method. The JSON object holds the current configuration of the plug-in instance, which will be saved in the Skydel configuration file paired with the version of the plug-in instance it was generated with. The version saved in the Skydel configuration file comes from the plug-in instance metadata at save time.

When loading a configuration file, Skydel will automatically instantiate all saved plug-in instance and restore their configuration via the `setConfiguration` method. It's possible for a plug-in instance to handle configuration backward compatibility since the configuration received is paired with a creation version.

### Example

See plug-in example [simple\_plugin](https://github.com/learn-orolia/skydel-plug-ins/tree/master/source/example/simple_plugin). It covers:

* Creating a user interface
* Sending notification messages
* Triggering the unsaved state
* Saving and loading of configuration

## SkydelPositionObserverInterface

### Real Time Positions

### Dynamic User Interface

### Example

See plug-in example [position\_observer\_plugin](https://github.com/learn-orolia/skydel-plug-ins/tree/master/source/example/position_observer_plugin).

## SkydelLicensingInterface

{% hint style="warning" %}
To use this role and see an example, contact Orolia Canada's technical support.
{% endhint %}

## SkydelInstrumentationInterface

## SkydelRapiInterface

