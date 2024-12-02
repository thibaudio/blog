---
title: "State Machines for Attacks"
date: 2022-07-31T22:00:49+02:00
draft: false
toc: false
images:
tags:
---

I'm currently implementing super attacks for my autobattler rogue like set in space.  
The goal is to have each turrets being able to perform unique super attacks on certain conditions.

I started with a simple MonoBehavior attached to the turret.
Then when I wanted to create a second super attack, I had to duplicate a bunch of the code. So I factored what I could in a parent class.

I couldn't implement the 3rd attack with the previous design, so I ended up deleting most of it and implementing a simple State Machine, with 2 states.

The 1st state is the IdleState, it's only job is to check if the condition needed to activate the special attack is met:
```csharp
public abstract class Super : MonoBehaviour
{
    private StateMachine stateMachine;
    private State superIdleState;
    private State superPerformState;

    private void Awake()
    {
        stateMachine = new StateMachine();
        superIdleState = new State("SuperIdleState", updateHandler: UpdateStateIdleState);
        // ...
        stateMachine.ChangeState(superIdleState);
    }

    private void UpdateStateIdleState()
    {
        if(CanSuperBePerformed()) stateMachine.ChangeState(superPerformState);
    }

    private void Update()
    {
        stateMachine.Update();
    }

    // Check function MUST be implemented
    protected abstract bool CanSuperBePerformed();
}
```

The 2nd state gives us the tool to implement the special attack it self:
```csharp
public abstract class Super : MonoBehaviour
{
    public float EffectDuration = 0.5f;
    private float currentEffectDuration = 0.0f;

    private void Awake()
    {
        stateMachine = new StateMachine();
        superIdleState = new State("SuperIdleState", updateHandler: UpdateStateIdleState);
        superPerformState = new State( "SuperPerformState", enterHandler: OnEnterPerformState, updateHandler: OnUpdatePerformState, exitHandler: OnExitPerformState);
        stateMachine.ChangeState(superIdleState);
    }

    // ...

    private void OnEnterPerformState()
    {
        currentEffectDuration = EffectDuration;
        EnableEffect();
        PerformEffectOnceAtStart();
    }

    private void OnUpdatePerformState()
    {
        currentEffectDuration -= Time.deltaTime;
        if(EffectDuration != -1 && currentEffectDuration <= 0.0f) {
            PerformEffectOnceAtEnd();
            stateMachine.ChangeState(superIdleState);
            return;
        }
        PerformEffectTick();
    }

    private void OnExitPerformState()
    {
        DisableEffect();
    }

    protected virtual void PerformEffectOnceAtStart() {}
    protected virtual void PerformEffectOnceAtEnd() {}
    protected virtual void PerformEffectTick() {}
    protected virtual void EnableEffect() {}
    protected virtual void DisableEffect() {}
}
```

This system gives us a lot of flexibility to create new super attack.  
I'm sure it will evolve again in the future so [subscribe to the newsletter](https://www.getrevue.co/profile/thibaudio) if you want to follow along!