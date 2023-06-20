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
Object intended for pooling require a component inheriting from PooledObject. Pools are automatically created a populated when requesting objects from the pool system.

```cs
// reference prefab inheriting from PooledObject
[SerializeField] private PooledParticleSystem _pooledParticlePrefab;
```
```cs
// request pooled copy of prefab from system
PooledParticleSystem ps = PoolSystem.Instance.Get(_pooledParticlePrefab);
// return object to pool when done
ps.Pool.Release();
```
