# IDOR Walkthrough – NightCorp Employee Portal

## Target

```text id="fsv9iw"
http://38.242.206.53:30000
```

## Vulnerability

The website is vulnerable to:

```text id="7owg2x"
Insecure Direct Object Reference (IDOR)
```

because user profiles can be accessed by changing the `id` parameter in the URL.

---

# Step 1 — Open the Website

Visit the target:

```text id="1cvvqj"
http://38.242.206.53:30000
```

You will see the NightCorp Employee Portal homepage.

<img src="https://i.ibb.co/HD04P87R/image.png" width="800">

---

# Step 2 — Open “My Profile”

Click on:

```text id="0q9d3u"
My Profile
```

The URL changes to:

```text id="t7kqes"
http://38.242.206.53:30000/?id=1005
```

<img src="https://i.ibb.co/hF4WZx68/image.png" width="800">

---

# Step 3 — Manipulate the ID Parameter

Now manually change the number in the URL.

Example:

```text id="i7b0gd"
?id=1004
?id=1003
?id=1002
?id=1001
```

<img src="https://i.ibb.co/G4RsQggQ/image.png" width="800">

<img src="https://i.ibb.co/XxGMVjC5/image.png" width="800">

---

# Step 4 — Access Other Employee Profiles

As you decrease the ID value, the application loads different employee records without authentication checks.

This confirms the IDOR vulnerability.

<img src="https://i.ibb.co/D0bKtXL/image.png" width="800">

<img src="https://i.ibb.co/99fKh6RZ/image.png" width="800">

---

# Step 5 — Reach the Admin Profile

Eventually one of the lower IDs reveals the Admin profile/panel.

<img src="https://i.ibb.co/NdwchX00/image.png" width="800">

---

# Step 6 — Capture the Flag

The flag appears on the admin page.

<img src="https://i.ibb.co/SDkfcZr8/image.png" width="800">

<img src="https://i.ibb.co/s9BLt01w/image.png" width="800">

---

# Flag

```text id="7s0zh1"
FLAG{...}
```

---

# Summary

* The application exposes internal user profiles through a predictable numeric parameter.
* No authorization checks are performed.
* By enumerating IDs, attackers can access privileged accounts and sensitive information.

This is a classic:

```text id="m3qjlwm"
IDOR (Insecure Direct Object Reference)
```
