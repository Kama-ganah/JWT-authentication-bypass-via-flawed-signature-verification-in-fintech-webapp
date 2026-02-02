# Overview
I evaluated the JWT-based authentication mechanism and discovered a critical flaw in signature verification. The server accepts tokens with the alg header set to "none", effectively bypassing signature validation. By crafting a JWT with arbitrary claims, I was able to impersonate the administrator and perform privileged actions, including deleting user accounts. This demonstrates a severe authentication bypass that allows complete account takeover.

# Methodology

Step 1: Logged in as a regular user and captured the JWT from session traffic.

Step 2: Decoded the JWT and modified the payload to escalate privileges (sub: "administrator").

Step 3: Changed the token header to alg: none and removed the signature.

Step 4: Sent the tampered token in the session cookie and successfully accessed the admin panel.

Step 5: Verified impact by deleting a selected user account using the elevated privileges.

# Conclusion

This assessment confirmed a high-severity JWT authentication bypass due to flawed signature verification. Remediation requires rejecting unsigned tokens, enforcing strong algorithm checks, and ensuring secure JWT library usage. Proper configuration and signature validation are critical to preventing unauthorized access and protecting sensitive resources.
