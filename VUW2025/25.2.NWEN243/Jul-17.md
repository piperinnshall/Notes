# Link Layer Services

Besides moving frames from one device to another device, what else does the
link layer do?

- Error detection and correction.
- Simple flow control.
- Medium access control - decides which device to transfer.

# Error Detection

- An error in transmitted data can be a:
    - single-bit.
    - burst.
- How to detect errors?
    - If we only transmit data, we cannot detect any errors.
    - However, we can:
        - Send meta data with the data that satisfies some special
          relationship.
        - Add redundant data.

If we only transmit the data we want to send, we don't get errors. We only get
1's and 0's.

We need to send something extra to do a check.

## Parity Check

- Simplest
    - Parity bit - ensure the sum is odd or even.
    - Can detect 1 bit error.
    - Cannot correct errors.
    - 7 bits + 1 parity.

Vertical Redundancy Check (VRC)

| 7 data bits | Sum of bits | even | odd |
|-|-|-|-|
| 0000000 | 0 | 0 | 1 |
| 0011101 | 4 | 0 | 1 |
| 1111111 | 7 | 1 | 0 |

## Longitudinal Redundancy Check (LRC)

Organize data into n, n bit words (e.g. 8)

Find the (even) parity of each word.

## Sending

- Create the data part of the frame.
- Compute error detection code over data.
    - Parity (cheap, good for quality media)
    - CRC (Cyclic Redundancy Code) is common for lossy media (WiFi).
- Add header containing the error detection code.
- Send one bit at a time via the physical layer.

## Receiving

- Read the frame (frame = header + data) one bit at a time using physical
  layer.
- Compute error detection code over data.
- Compare received EDC with recomputed EDC.
- Reject if do not match.

## A quick note on Error Correction.

Instead of error detection code, add error correction code.
- Add extra bits that allow the bit flip to be detected and corrected.
- Hamming codes are one technique.
- Trade off between cost of re transmission, frequency of error and
  overhead of number of bits..
- The worse the media, the better the error detection/correction required.

Look at what the protocol aims to achieve, and how much you want to put into
the design.

On a rainy day, when the air is very humid, there is a higher chance of your
signal getting corrupted. Water can affect the signal.

## Medium Access Control

- channel partitioning.
    - divide channel into smaller “pieces” (time slots,
      frequency, code).
    - allocate piece to node for exclusive use.
- random access.
    - channel not divided, allow collisions.
    - “recover” from collisions.
- “taking turns”.
    - nodes take turns, but nodes with more to send can take.
      Longer turns.

### Channel partitioning MAC protocols (1)

Shared broadcast channel.

- Problem:
    - two or more simultaneous transmissions by nodes: interference.
    - if node receives two or more signals at the same time:
      collision.
- Solution
    - multiple access protocol.

Try to find the little pause between people talking.

If 2 or more devices transmit at the same time, you might get interference.

### Multiple Access Protocol

- Distributed algorithm that determines how nodes share channel, i.e.,
  determine when node can transmit.
- Communication about channel sharing must use channel itself!
- No out-of-band channel for coordination.

