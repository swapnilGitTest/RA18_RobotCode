# Creating AutoMove Components

## AutoMoveMove
First, create a new class that implements `AutoMoveMove`:
```java
public class TalonMove implements AutoMoveMove {
    
}
```
Create a constructor that takes and stores the objects that are used:
```java
public class TalonMove implements AutoMoveMove {
    TalonSrxWrapper talon;

    public TalonMove(TalonSrxWrapper talon) {
        this.talon = talon;
    }
}
```
The `setArgs` function takes a map that describes how a move may vary.

In this example, we just want a power to set the talon to.

Implement the `setArgs` function:
```java
public class TalonMove implements AutoMoveMove {
    ...
    private double power;

    @Override
    public void setArgs(Map<String, String> args) {
        power = (double) args.get("power");
    }
}
```
The three parts of running a move are `start`, `run`, and `stop`.

`start` and `stop` are run once at the beginning and end of a move respectively.
`run` is run each code cycle, possibly directly after `start` or before `stop`.

Running a motor has no special initialization, so we'll leave it empty:
```java
public class TalonMove implements AutoMoveMove {
    ...
    @Override
    public void start {}
}
```
`run` will run the motor, and `stop` will stop it when the move ends:
```java
public class TalonMove implements AutoMoveMove {
    ...
    @Override
    public void run {
        talon.set(ControlMove.PercentOutput, power);
    }

    @Override
    public void stop {
        talon.set(ControlMove.PercentOutput, 0);
    }
}
```
And that's it, the whole file would look like this:
```java
//package and imports

public class TalonMove implements AutoMoveMove {
    TalonSrxWrapper talon;

    public TalonMove(TalonSrxWrapper talon) {
        this.talon = talon;
    }

    @Override
    public void start {}

    @Override
    public void run {
        talon.set(ControlMove.PercentOutput, power);
    }

    @Override
    public void stop {
        talon.set(ControlMove.PercentOutput, 0);
    }
}
```