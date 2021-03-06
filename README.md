# Unity Event System Width Scriptable Objects

Link Demo: [Event System With Scriptable Objects (Unity Play)](https://play.unity.com/mg/other/demo-event-system-with-scriptable-objects)  

#### Blue Voxel Inside Team
1. José Luis Aguilera Luzania
2. Ramón Antonio Sanchez Madrid

## Objetives
- Create an easy-to-use and customizable event system in Unity to remove strong reference dependencies between GameObjects.
- Provide a type of generic event that can be specialized for any type of data.

## Observer Pattern
Is a behavioral design pattern that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.

Please see: [Observer (refactoring.guru)](https://refactoring.guru/design-patterns/observer) for a full explanation.

## Content
By default the package has five predefined events for data types: `void`, `int`, `float`, `bool`, `string`.
- `VoidEventSO`: It is used when it is not necessary to send data to listeners.
- `IntEventSO`: It is used when it is necessary to send data of type int to listeners.
- `FloatEventSO`: It is used when it is necessary to send data of type float to listeners.
- `BoolEventSO`: It is used when it is necessary to send data of type bool to listeners.
- `StringEventSO`: It is used when it is necessary to send data of type strings to listeners.

## How to use it?
### Setup listeners
1. First declare the intEvent variable in your script of the type you need.
```C#
public IntEventSO intEvent;
```

2. Create a callback function that will be called every time the event is invoked.
```C#
private void OnInt(int value) 
{
	// Do something.
}

```

3. Register the callback function in the event in the OnEneable function.
```C#
private void OnEnable() 
{
	intEvent.AddObserver(OnInt);
}
```

4. Unregister the callback function in the event in the OnDisable function.
```C#
private void OnDisable()
{
	intEvent.RemoveObserver(OnInt);
}
```

### Setup subject
1. First declare the attribute in your script of the type you need.
```C#
public IntEventSO intEvent;
```

2. Use the Invoke(T value) method when you want to notify listeners about something.
```C#
// code...
intEvent.Invoke(value);
// more code...
```

### Create the event asset
1. You can create event objects using the "Event SO" submenu in the create menu.  
![](Images/Assets%20Events%20SO.png)


1. Assign the asset in the fields of the component that listens or invokes. You can also invoke the event using a button.

Invoke the event using a button.  
![](Images/Int%20Event%20BTN.png)

Assign the assets to a script.  
![](Images/Demo%20UI.png)

## How to create a new type of event?
For this example let's make an event that sends a GameObject as a value when invoked.

1. First we need to create the `GameObjectEventSO` script.

2. If you want to create your own event with its own data type you must first import the namespace
```C#
using Plugins.Event_System_SO.Scripts;
```

3. Instead of inheriting from `MonoBehaviour`, we inherit from `EventOS` and between <> we specify the type of data that will be sent when the event is invoked, in this case GameObject.
```C#
public class GameObjectEventSO : EventSO<GameObject>  
{  
}
```

4. Now we add the attribute `CreateAssetMenu` where we specify the submenu "Event SO" and the item "GameObject Event".
```C#
[CreateAssetMenu(menuName = "Events SO/GameObject Event")]
public class GameObjectEventSO : EventSO<GameObject>  
{  
}
```

5. Now we can create our asset events that send GameObjects to listeners. We can also use buttons to invoke the events!  
![](Images/GameObject%20Event%20BTN.png)

## Images
![](Images/Demo%20Scene.png)

## Dependencies
- TextMeshPro
