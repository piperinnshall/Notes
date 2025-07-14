# Threat Modeling

Apply, compare and contrast brainstorming techniques.
- Misuse cases.
- Personas.
- Security cards game.

Start thinking about the threats that might impact the applications or systems
that you build and how you might protect against them.

## Definitions

- Asset.
    - Something that should be protected.
- Vulnerability.
    - Weakness or lack of protections.
- Threat.
    - Something that could negatively impact an asset.
        - A hacker trying to break into accounts.
- Security Controls aka “mitigation”.
    - Protect against threats, reduce vulnerability.
        - Password rules.
        - Firewalls.
- Risk.
    - The possibility that a threat will exploit a vulnerability to
      harm an asset.
        - Risk = Threat * Vulnerability.

Mitigation strategies:
- Account lockouts.
- Multi factor authentication.

## Why?

- Non-compliance.
- Weight/Cost of Risk Realization.
- Data Loss .
- Monetary Cost.
- Reputation.
- Weight/Cost of Countermeasures.

## When?

- After Implementation.
    - High cost to fix issues.
    - More vulnerabilities = more risk.
- During Development
    - Consider security during system design and development to reduce vulnerabilities.

## Question

Which is better?
- During.
- At the end.
- Something else.

## How? Threat Modeling

- Analyzing the Application/System
    - What does the system do?
- Determining Threats
    - What could go wrong?
- Addressing Threats
    - What can you do?

## Threat Modeling techniques

Unstructured
1. Misuse cases.
2. Persona non Grata.
3. Security cards.
4. Privilege escalation game.

Structured
1. STRIDE, DREAD and friends.
2. Attack trees.
3. Attack libraries.
4. PASTA.
5. VAST.
6. Trike.
7. OCTAVE.
8. NIST.

### Brainstorming

- Experienced experts in a room.
- Whiteboard, papers
- Quality bounded by experience of brainstorming and amount of time spent
- brainstorming.
    - Techniques:
    - Persona non Grata.
    - Use cases.
    - Security cards.

## Use cases

- Requirements - what the system should do, service or services that are
  provided, and constraints on operations.

- Use case - capture, model, and specify requirements.
    - Behaviors system may perform.
    - Interaction with actors. 
    - Actors are human users or other systems.
- We’re using the simplest version that is similar to what is known as a
  user story.
- Example:
    - Use case: Pay Fees
    - Actors: Student, University website, Financial Institution.
    - Steps:
        1. Student opens pay fees page on the University website.
        2. Student enters credit card details.
        3. University website passes amount and credit card details
                       to Financial Institution.
        4. Financial institution processes payment as long as valid
                       credit card details.

## Misuse cases


- A misuse case is the evil twin of a use case.
- A misuser is a bad actor.
- Misuse cases and use cases are shown together.
- The association between a misuse case and a use case can either be a
  “threatens” or a “mitigates” relationship.

