SMACH
=====

SMACH is a task-level python execution framework for rapidly composing complex
robot behaviors.

This fork adds rudimentary structural coverage collection to smach.
Specifically, structural coverage will be collected for each StateMachine object
created and executed in the program. Nested StateMachines are not supported, but
should collect coverage data separately, treating inner StateMachines as if they
were a simple state. The coverage data collected is simply the states executed,
and their outcomes.

Coverage data is stored in the CWD, in files named `.scov_I`, where I is an
integer counter for each StateMachine object instantiated by the program. These
will be numbered according to their instantiation order in the program. A simple
example with only a single StateMachine will produce the file `.scov_0`. Note that
subsequent executions will overwrite this file.

Usage
-----

Coverage data will be automatically collected provided at least one StateMachine
is executed in a program. Coverage data is written to files when execution
finishes - i.e. when the StateMachine returns an outcome.

The most straightforward method to use this modified version of smach is to copy
the smach source folder (`smach/src/smach`) to the directory of your smach
application.

After running the program, you may view a simple coverage report by running the
smach_coverage_report python script, as follows:

```
./smach_coverage_report.py .scov_0
```

This will give some simple statistics on the percentage of outcomes achieved, as
well as a list of all uncovered outcomes for each state.

By renaming the coverage data file and running the code again, you may combine
output by specifying multiple data files as arguments to the script. Note that
the reporting script expects all coverage data files supplied to originate from
the same state machine - i.e. the list of outcomes and states must be identical.

```
./smach_coverage_report.py .scov_0 .scov_0_test1 .scove_0_test2
```
