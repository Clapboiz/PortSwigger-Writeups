### Challenge 1: OS command injection, simple case
### Challenge 2: Blind OS command injection with time delays
### Challenge 3: Blind OS command injection with output redirection
### Challenge 4: Blind OS command injection with out-of-band interaction
### Challenge 5: Blind OS command injection with out-of-band data exfiltration

**`Command substitution`** is a feature of shell scripting that allows you to take the output of one command and use it as the input for another command. In Unix and similar operating systems, command substitution is done by placing the command within backticks (`) or the $(...) syntax.

Here's how it works:

+ When the shell encounters a portion of a command within backticks or the $(...) syntax, it executes that portion of the command first.
+ After the sub-command is executed, the shell takes its output and replaces the original backtick or $(...) part with this output.
+ The main command then continues execution with the output of the sub-command as part of the command.

```
echo The date is `date`
```

The shell will perform the following steps:

+ Execute the date command, obtaining the output (for example: "Thu Mar 4 10:22:36 PST 2021").
+ Replace the date command within the backticks with this output.
+ Execute the echo command with the replaced output, for instance: "The date is Thu Mar 4 10:22:36 PST 2021".
