## Topic `movement`

By joining this topic, you can move your entity and also observe others as they move theirs.

_Hint: Movement is currently completely client based. This is very beneficial for the server in terms
of workload and code complexity, but may change in the future. Also, the server aims to at least do sanity
checks on the client updates. Since the client updates are async, you will only notice the real change
when the server propagates it back to you._

---

Asynchroneous client requests.

```
update
- position        // the new position
 - x
 - y
 - plane
- goal            // the point towards we are moving
 - x
 - y
 - plane
- move_type       // movement type  (0-10)
- velocity        // the new velocity coefficient (-1-2)
```

---

Asynchroneous server updates.

```
update
- entity          // event sender
- position        // the new position
 - x
 - y
 - plane
- goal            // the point towards we are moving
 - x
 - y
 - plane
- move_type       // movement type  (0-10)
- velocity        // the new velocity coefficient (-1-2)
```

---
