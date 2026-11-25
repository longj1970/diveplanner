# Bo'ness Sub Aqua Club – Dive Plan Generator

A single-page website that builds a full dive expedition plan from three inputs: **dive site**, **date** and **meeting point**. It follows the layout of the club's Twin Piers expedition plan.

## What it fills in automatically

| Section | Source |
|---|---|
| Drive time and departure time | Meeting point looked up on OpenStreetMap, route from OSRM |
| Dive schedule | You enter the meeting time and meeting point for each plan. **Standard** schedule: dive 1 enters the water at 10:00, dives up to 45 min, next dive 1 h 15 min after leaving the water. **Non-standard**: set your own dive 1 time (or time it to high or low water), dive length and gap for that plan. Drive time comes from live routing; the plan estimates your arrival and warns if it leaves less than an hour on site before dive 1 |
| Weather summary and hourly table (temperature, rain chance, wind, gusts, sunrise and sunset) | Open-Meteo forecast (about 16 days ahead) |
| Tide times (HW/LW) and tide state at each dive | Admiralty UK Tidal API if a key is set; otherwise an estimate from the Open-Meteo ocean model |
| Sea temperature and waves | Open-Meteo marine |
| Risk assessment | Standard club hazards, plus hazards triggered by the forecast (cold, wind, swell, fading light, high water) and the site's own hazards |
| what3words | Saved per site, or looked up with an API key, or a what3words link from the coordinates |
| Google Maps | Site link, driving directions from the meeting point, embedded map |
| Nearest A&E, and any closer minor injuries unit | OpenStreetMap, ranked by driving time |
| Site reference | Link to the site on divemap.uk |
| Conditions at a glance | Colour-coded go/no-go panel at the top of the plan: wind, rain, temperature, daylight, sea state, tides, divers and depths, with an overall verdict |
| Buddy depth checks | Each group's limit is set by its shallowest-qualified diver (ScotSAC grades from the **Divers** register). Over-limit groups are flagged in the form and the plan, and a blank depth defaults to the group limit |
| Emergency Action Plan | Site location to read out (coordinates, what3words, parking), who to call and when, immediate actions for DCI, missing diver procedure. Names the Dive Marshal, First Aider and Oxygen Administrator from the roles |
| Dive Marshal Slate | A printable record for each dive: buddy groups, planned max depth, air in/out, time in, due out, time out, max depth, plus an ICE contacts table. Print it on its own with **Print dive slate** |
| Equipment checklist | Club list, plus extra items for the conditions (cold, rain, low light) |

Team roles, buddy pairings and a dive map image are optional. Leave them blank to fill in later. Roles and meeting points are remembered between uses.

The plan can be edited on screen, then downloaded as a **Word (.docx)** file, printed or saved as PDF, or copied as text.

## Version history

- **v1.9** – Shore or boat dive choice (preset from the site library). Boat dives add the launch point and the boat and skipper, drive time to the launch point, boat hazards, VHF Channel 16 in the Emergency Action Plan, boat kit, a skipper role and a boat cover note on the slate.
- **v1.8** – Buddy pairings entered as rows (diver name, pair number, optional max depth), starting with two rows, with **+ Add diver** for more. Divers without a buddy are flagged.
- **v1.7** – Training section: a guide to each part of the dive plan and a 10-question multiple-choice quiz (pass mark 8/10). Fixed full-screen panels on iPhone.
- **v1.6** – Meeting time and point are entered for each plan. Standard 10:00 schedule or a non-standard schedule. Arrival is checked against the first dive.
- **v1.5.1** – Meeting point lookup fixed (searches near the dive site, handles misspellings) and shows the matched address.
- **v1.5** – Schedule reworked around a 10:00 first dive: arrive on site 1 hour before, 1 h 15 min from leaving the water to the next entry, with debrief, break, briefing and buddy checks shown.
- **v1.4** – iPhone app: installs from Safari with Add to Home Screen, phone layout with bottom tabs, Word file through the iOS share sheet, plans saved on the device and readable offline.
- **v1.3** – Diver register with ScotSAC grade depth checks (CR-003) and conditions-at-a-glance panel (CR-004).
- **v1.2** – Dive Marshal Slate (CR-001) and Emergency Action Plan (CR-002). New setting: max dive time on slate.
- **v1.1** – Progress bar, required-field highlighting, club logo.
- **v1.0** – First release.

## Installing on an iPhone (no App Store)

The planner is a web app. Once it's hosted, it installs from Safari and behaves like an app.

**1. Put it online (one-off, about 2 minutes).** iPhones only install web apps from a secure (https) address, so the folder must be hosted. The free, easiest option:
- On a computer, go to **app.netlify.com/drop**.
- Drag the whole `boness-dive-planner` folder onto the page.
- Netlify gives you an address such as `https://something.netlify.app`. Create a free account to keep it, and rename it in Site settings, for example `boness-dive-planner.netlify.app`.

GitHub Pages or the club website also work. Upload every file in the folder, keeping the `icons` folder.

**2. Add it to the iPhone.**
- Open the address in **Safari**. Other browsers on iPhone can't add web apps in the same way.
- Tap the **Share** button (the square with an arrow), scroll down and tap **Add to Home Screen**, then **Add**.
- The club logo appears on the home screen as "Dive Planner".

**3. Using it.**
- **Plan:** fill in the site, date and meeting point and tap Generate. The plan opens on the **Result** tab.
- **Share Word file:** opens the iPhone share sheet, so you can save to Files, email it or send it on WhatsApp.
- **Saved:** every plan is stored on the phone. Generate it at home, then open it at the dive site with no signal.
- **Divers, Sites and settings (gear icon):** stored on the phone. The installed app has its own storage, separate from Safari, so re-enter them or use **Import library** for sites.
- **Updates:** replace the files on Netlify (drag the folder again onto the same site's Deploys page). The app picks up the new version next time it opens with signal.

Generating a new plan needs signal, because the weather, tides, routes and hospitals are fetched live.

## Putting it online

It is one file (`index.html`) with no server code. Any of these will host it:

- **Netlify Drop:** go to app.netlify.com/drop and drag the folder in. You get a link straight away.
- **GitHub Pages:** create a repository, upload `index.html`, then turn on Pages in Settings.
- **The club website:** upload `index.html` as a page or file.

You can also double-click `index.html` to run it from your own computer.

## Training

The **Training** button (or the **Learn** tab on a phone) opens a guide for new members. It covers each of the 13 sections of a dive plan: what goes in it, why it matters and where the planner gets the information. It ends with a 10-question multiple-choice quiz, with feedback after each answer and a score at the end. The pass mark is 8/10, and each device remembers its best score. Questions and answers are shuffled each time.

The Diving Officer can edit the guide and the questions in the `TRAINING` section near the top of the script in `index.html`.

## Divers register

Use **Divers** to record each member's name and ScotSAC grade: Branch Diver 15 m (12 m under 14), Sport Diver 30 m, Master Diver 40 m, First Class Diver 40 m. Set **Own limit** for deeper or other-agency qualifications. Names in the buddy pairings are matched by full name or by first name when that is unique. The register is saved in this browser only.

## Site library

Use **Site library** to add the club's regular sites. Each site stores:

- location, max depth, dive type
- divemap.uk link
- what3words for the site and the parking
- access notes (parking, carrying kit, entry)
- dive route
- site-specific hazards

The site location box accepts any of these formats:
- `56.19439, -4.77101`
- `N 56° 11.663' W 4° 46.260'` (the format divemap shows, with a copy button)
- a Google Maps link

Twin Piers is preloaded with the details from the existing club plan. The A-Frames, Craggen, Midway and Torpedos are preloaded with coordinates and a short description. Add their route and access notes when you have them.

The library is saved in each person's browser. To share it, use **Export library** and send the file to other members, who use **Import library**. To make sites permanent for everyone, paste the exported entries into the `SEED_SITES` list near the top of the script in `index.html`.

## Optional keys (Club settings)

- **Admiralty UK Tidal API (UKHO):** a free "Discovery" key gives official HW/LW times and heights above chart datum for the nearest tide station, up to 7 days ahead. Recommended.
- **what3words API:** converts any site's location to a 3-word address automatically.

Keys are saved only in the browser where you enter them.

## Limitations to know

- **Tides without a UKHO key are estimates.** The ocean model doesn't cover sea lochs or the inner Clyde and Forth. The page uses the nearest open-water point and says how far away it is. Times are usually close, but heights are relative to mean sea level, not chart datum. Always confirm with Admiralty EasyTide.
- **Forecasts change.** Regenerate the plan the day before the dive. For dates more than about 16 days ahead the plan says the forecast isn't available yet.
- **divemap.uk has no public API** and only allows its own website to query its data, so the page links to divemap rather than copying its content. Copy depths, hazards and coordinates from divemap into the site library.
- **Hospital data comes from OpenStreetMap tags.** Check the A&E listed before relying on it. For example, Vale of Leven is a minor injuries unit, not an A&E.
- The free services used (Nominatim, OSRM, Open-Meteo) are meant for low-volume use. That suits a club, but not a high-traffic public site.
