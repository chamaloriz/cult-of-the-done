---
title: Take control of the youtube feed, but first let's take the data.
created: 2025-10-05
tags:
  - success
---

I'm building a self-hosted youtube feed but the first step is about the data you have.

Google gives you a way to export your [youtube data](https://support.google.com/accounts/answer/3024190), the CSV files that it gives you back looks like this.

```csv
UC-0078V3b7nUsAQodzIbOug,http://www.youtube.com/channel/UC-0078V3b7nUsAQodzIbOug,dummesaulol
UC-0kTRFR6xEwI4lah9CzFHA,http://www.youtube.com/channel/UC-0kTRFR6xEwI4lah9CzFHA,Max Kolo
UC-1rx8j9Ggp8mp4uD0ZdEIA,http://www.youtube.com/channel/UC-1rx8j9Ggp8mp4uD0ZdEIA,TheCGBros
...
```

The data from it is limited and to get a bit more info about a channels like the thumbnail and some other stats you can use your free tokens on the [youtube official API](https://developers.google.com/youtube/v3).

```bash
# to make the request you need to get an api token from here : https://console.cloud.google.com/apis/credentials
# the channel_id can be found in the CSV file.
curl -X GET "https://youtube.googleapis.com/youtube/v3/channels?part=statistics,snippet,brandingSettings&id={channel_id}&key={api_key}"
```

Now that we have the overall channel data, we need to fetch the youtube videos and for that we can use the RSS feed of each channel.

```bash
curl -X GET "https://www.youtube.com/feeds/videos.xml?channel_id={channel_id}"
```