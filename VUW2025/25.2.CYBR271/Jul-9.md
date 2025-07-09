# Secure Coding Principles

- These principles have been known for a long time.
- They have evolved over time.
- Mainframes -> Web applications.

## 13 Secure Coding Principles

1. Minimize attack surface
2. Defense in depth
3. Don’t reinvent the wheel
4. Economy of mechanism
5. Separation of duty
6. Open design 
7. Secure the weakest link
8. Least privilege
9. Fail securely 
10. Psychological acceptability
11. Validate inputs
12. Secure data at rest
13. Avoid bypass attacks

### Minimize attack surface

Attack surface describes all the different points where an attacker could get
into a system and where they can get data out.

Consider a place to wait out the Zombie apocalypse. Where would you want to go
that has a smaller attack surface?

The Attack Surface of an application is:
1. The sum of all paths,
2. The code that protects these paths,
3. all valuable data used in the application,
4. the code that protects these data

[OWASP Attack
Surface](https://cheatsheetseries.owasp.org/cheatsheets/Attack_Surface_Analysis_Cheat_Sheet.html)

### Defense in Depth

***Use layered security defenses.***

- There many ways to defend your application.
- A given defense may fail.

What might go wrong?
- Security is very difficult to get right.
- Negligence is responsible to up to 1/3 of exploits.
- Performance issues.

### Don’t Reinvent the Wheel

***There is a lot of code available.***

When there is a good security code available, don’t try to create your own.

- Examples:
     - Cryptography is difficult to implement well.
        - CYBR 372 Applications of Cryptography.
    - Web application frameworks simplify development.
        - Assignment 3 covers this issue.

### Economy of Mechanism

***Security mechanisms should be as simple as possible***

"Entities should not be multiplied without necessity" (William of Occam)

No more things should be presumed to exist than are absolutely necessary.

I.e., the fewer assumptions an explanations of a phenomenon depends on, the
better the explanation

The KISS adage, Keep It Simple Stupid:
- Complicated is the enemy of security.
- Simple security constructs.
- Don't implement unnecessary security constructs.

### Separation of Duty

***Privileges should not be granted based on a single condition.***

A simple example is the need for two signatures in order for a bank to make a
payment.

Examples:
- Two factor authentication.
- Accounting systems.

### Open design

***The security of a component or system should not depend on the secrecy of
the design or implementation.***

Keys: the secret data that must be protected.

Also known as avoiding "Security by Obscurity“.

### Secure the weakest link.

***Attackers will attack the weakest security point in the application.***

Adversaries will expend the least amount of effort possible to penetrate a
system.

Threat Models will lead you to the weakest areas.
- Invest in re-mediating weakest security defenses.
- There will always be a new weakest link.
-  Attackers will go after weakest links simply because they are easy.

What could go wrong?

Where are we vulnerable?

What is the most likely path for an attacker to attack a system.

### Least privilege

***A subject should only be granted only the privileges needed for an
operation***

Least Privilege is a concept that means that at any given application state,
the user will operate at the lowest level of access rights possible.

A program should be given only those privileges it needs in order to satisfy
its requirements:
- Do you run your local desktop as an Administrator user?
- On Linux, running services as root or with SetUID permission bit set has
  the same effect.

### Fail securely

***Handle all failures securely and return the system to a proper state.***

Problem: Error messages can disclose information valuable to an attacker.

Example:
- Java stack trace.
- Internal Server Error.

### Psychological acceptability

***Security mechanisms should not make the resource more difficult to access
than if the security mechanism were not present.***

If users find a security feature frustrating they will to to bypass, or worse,
disable it.

Password requirements: Design security that is effective, but also user
friendly.

Compare two password schemes:
- Random numbers.
- Passphrases.

Humans are bad at memorizing random strings.

### Validate Inputs

***All inputs should be treated as untrustworthy.***

Never trust user input, until it is validated.

Hackers frequently use malicious inputs to break security.

- There are many vulnerabilities that are created or worsened by using
  non-validated inputs in code constructs.
- In addition, if you allow inputs that are incorrect for any reason into
  your system, you risk its integrity.

### Secure Data at Rest

***Data at rest must be protected to meet security requirements.***

If someone gains physical or logical access to storage, they can extract that data.

Doctors have access to patient records, but no way to extract these records.

This is a very difficult problem.

### Avoid Bypass Attacks

***Attacks that bypass authentication or authorization gates are among the most dangerous.

Consider “Forgot my password” as a way to bypass authentication.

The login/password/forgotten-password system must be designed carefully.
- Prevent information leakage.
- Strong configurable passwords.
- Strong encryption.
- No bypass opportunities.

