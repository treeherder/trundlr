## trundlr
--------

A free, open-source application to help with the collection and distribution of otherwise wasted food.

#### Objective:
--------
  * To provide trundlr as a utility for drivers in extension to the extant android-oriented service.
  * Provide a standalone call-in service to relieve the organizer's burden.
    * intelligently track volunteer drivers sign ups
    * confirm drivers on day-of
    * organize back-up driver volunteers if needed
    * forward a digest version to organizers in a timeely fashion
    * built in throttle mechanisms controlled by organizer, with backup and default organizer settings

#### Rationale:
--------
Because our current model (based on food-not-bombs) for a distribution newtork requires an untenable amount of human industry to keep running on a week-to-week and day-to-day basis, trundlr should provide some inteligent service that the organizer can rely upon to self-organize volunteers and their various problems with temporality and spacial precision.

##### Current Model

1. Drivers sign-up according to availablity in a pool.
2. A donor chooses a day and time, and provides a count.
3. The pool of available drivers is reckoned against the count given.
4. Available reception locations are identified, and their need is tallied.
5. A number of drivers, considering capacity and need for locations are asled to come, with some on standby.
6. Volunteers, organizers, and donors meet at donation location and distribute food.
7. Vehicles self report a tally, and in some cases return a recipt.


### how this program works
----
trundlr's backend services work by reverse proxy over [nginx](http://nginx.org/en/download.html):
##### nginx config:
from `/etc/nginx/sites-available/default` :

    server {
    listen 80;

        server_name trundlr.roastrev.com;

            location / {
                   proxy_pass http://localhost:9001;
                   proxy_http_version 1.1;
                   proxy_set_header Upgrade $http_upgrade;
                   proxy_set_header Connection 'upgrade';
                   proxy_set_header Host $host;
                   proxy_cache_bypass $http_upgrade;
      }
    }

[twilio] (https://github.com/twilio) obviously has the most stable SMS and voice integration, and their services are affordable, given limited use.
