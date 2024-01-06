# WPILib Commands
Commands are one of the two core concepts in WPILib. 

## `extends CommandBase` vs `implements Command`: What is the difference?
This difference was added in the rewrite of WPILib a few years ago, and it was done to make it easier to implement more advanced functionality. We default to using the `CommandBase` class because it implements some utility methods (such as `addRequirements`) and has default implementations of the core command lifecycle methods.

# Command Structure
**See WPILib Docs:** https://docs.wpilib.org/en/stable/docs/software/commandbased/commands.html

### What is a dependency?
Commands require subsystems in order to actually work. Since the robot is capable of having multiple commands run at once, we need to have a way for the system to know what commands control what subsystems. Without this, two or more commands could control one subsystem. This could lead to a near infinite number of different bugs.  

## Properly Handling Dependencies
To prevent this class of bugs, the Scheduler checks what dependencies (i.e. subsystems that a command uses when it runs) a Command has *before* it is initialized. For this to work properly, we have to explicitly tell the scheduler what dependencies a command has. Since we default to using `extends CommandBase` for our commands, we have the `addRequirements` method that is built in.
```java
...

addRequirements(Subsystem1, Subsystem2);

...
```