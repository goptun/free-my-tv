# The Calendar reads a secret iCal link, not the Google Calendar API

The Calendar Widget reads one or more secret iCal addresses (Google Calendar: Settings → "Secret address in iCal
format") set in `config.properties` as `calendar_ics`, instead of signing in with Google (OAuth and the Calendar API).
A TV has no comfortable way to sign in, OAuth needs an app registered with Google and tokens kept on the device, and
the Widget only reads. The link is treated like the TMDB key: the person pastes it, it never goes in a chat or a
commit, and generic builds have none.

## Consequences

- Anyone with the link can read that calendar; leaking it means resetting it in Google Calendar.
- Google refreshes the iCal feed with a delay (minutes to hours), so a just-created Appointment may show up late.
- The app must expand recurring Appointments itself (RRULE, EXDATE, RECURRENCE-ID) and handle time zones.
