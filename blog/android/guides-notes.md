## Saving and restoring transient UI state

https://developer.android.com/guide/components/activities/activity-lifecycle#saras

an activity's UI state to remain the same
- a configuration change, such as rotation or switching into multi-window mode
- temporarily switch away from your app to a different app and then come back to your app

system constraints
- preserve the user's transient UI state using a combination of `ViewModel`, `onSaveInstanceState()`, and/or local storage.

The saved data that the system uses to restore the previous state is called the **instance state** and is a collection of key-value pairs stored in a `Bundle` object.

A `Bundle` object isn't appropriate for preserving more than a trivial amount of data because it requires serialization on the main thread and consumes system-process memory. 

Note: `onSaveInstanceState()` is not called when the user explicitly closes the activity or in other cases when `finish()` is called.
