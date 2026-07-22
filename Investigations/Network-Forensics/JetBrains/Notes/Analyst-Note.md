# Analyst Notes

## What helped me solve this investigation?

- HTTP POST filtering
- Follow TCP Stream
- Statistics → Conversations

---

## Challenges

Initially I inspected all HTTP packets, which produced a large amount of noise.

Filtering HTTP POST requests significantly reduced the investigation scope.

---

## Key Takeaways

Small artifacts can reconstruct an entire attack.

Following TCP Streams is one of the fastest methods for understanding attacker behavior.
