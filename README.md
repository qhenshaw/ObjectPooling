# Object Pooling
[![Unity 2021.3+](https://img.shields.io/badge/unity-2021.3%2B-blue.svg)](https://unity3d.com/get-unity/download)
[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE.md)

A lazy initialized object pooling system for Unity3D.

## System Requirements
Unity 2021.3+. Will likely work on earlier versions but this is the version I tested with.

## Installation
Use the Package Manager and use Add package from git URL, using the following: 
```
https://github.com/qhenshaw/ObjectPooling.git
```

## Usage
Prefabs intended for pooling require a component implementing IPoolable. Pools are automatically created and populated when requesting objects from the pool system.
A generic base class implementation of IPoolable is included as PooledObject.
No scene setup is required, simply get a reference to an IPoolable implementing class and request it from the PoolSystem:

```cs
// reference prefab inheriting from PooledObject
[SerializeField] private TimedPooledObject _pooledPrefab;
```
```cs
// request pooled copy of prefab from system
TimedPooledObject pooled = PoolSystem.Instance.Get(_pooledPrefab);
// return object to pool when done
pooled.ReturnToPool();
```

The current status of a PooledObject can be checked with IsInPool.
An example script for adding a timer to return the object can be seen here:
```cs
using UnityEngine;
using ObjectPooling;

public class TimedPooledObject : PooledObject
{
    [SerializeField] private float _duration = 2f;

    private float _spawnTime;

    private void OnEnable()
    {
        _spawnTime = Time.time;
    }

    private void Update()
    {
        if (IsInPool) return;
        if (Time.time > _spawnTime + _duration) ReturnToPool();
    }
}
```