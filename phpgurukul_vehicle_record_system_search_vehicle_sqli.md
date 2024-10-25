# SQLi vulnerability from phpgurukul Vehicle Record System 1.0 (search-vehicle.php)


**Affected Project**: Vehicle Record System 1.0

**Official Website**: https://phpgurukul.com/vehicle-record-system-using-php-and-mysql/

**Version**: 1.0

**Related Code file**: search-vehicle.php

## Vulnerability Description

When searching for vehicles, POST parameter 'searchinputdata' is 'Generic UNION query (NULL) - 1 to 20 columns' injectable.


## Demonstration

Users can search for vehicle as such:

![Screenshot from 2024-10-26 01-15-25](https://github.com/user-attachments/assets/68dad7bb-ad8f-4fd5-a826-4736f2556544)

Intercept the status check traffic using Burp Suite:

![Screenshot from 2024-10-26 01-17-20](https://github.com/user-attachments/assets/81e04cd7-77c0-438d-867e-ef999d22ff3c)

Now copy-paste the traffic and save it in to `search.req` and run `sqlmap` against it: `sqlmap -r search.req --batch`

`sqlmap` automatically exploit the vulnerability:

![Screenshot from 2024-10-26 01-17-58](https://github.com/user-attachments/assets/4fb25b9f-6a7c-4d66-a191-a07bd83fb31b)
