# albumrank

Find your top albums on Spotify, ranked by the percentage of each album's tracks you've liked.

<img width="1504" height="750" alt="Screenshot 2026-03-31 at 1 49 03 AM" src="https://github.com/user-attachments/assets/b548aafe-cc7f-40bc-848c-76dd06af74e7" />


## how it works

It fetches your entire liked songs library via the Spotify API, groups tracks by album, and calculates what percentage of each album you've liked. A 12-track album where you've liked 10 songs ranks higher than a 20-track album where you've liked 8.

The "min tracks liked" filter is useful for cutting out albums where you only liked one random song — try setting it to 3+ or 5+ to surface albums you genuinely love front to back.

## setup

### 1. create a spotify app

1. Go to [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) and log in
2. Click **Create app**
3. Fill in any name and description
4. Under "Which API/SDKs are you planning to use?" select **Web API**
5. In the Redirect URIs field add: `http://127.0.0.1:8888/album-rank.html`
6. Save, then copy your **Client ID** from the app overview page

### 2. serve the file locally

Clone the repo and serve it with Python:

```bash
git clone https://github.com/kush-ptl/album-rank.git
cd album-rank
python3 -m http.server 8888 --bind 127.0.0.1
```

Then open your browser to:

```
http://127.0.0.1:8888/album-rank.html
```

### 3. connect

Paste your Client ID into the field and click **Connect Spotify**. You'll be redirected to Spotify to authorize, then brought back and the fetch will start automatically.

## notes

- **No backend required.** Auth uses the [PKCE flow](https://developer.spotify.com/documentation/web-api/tutorials/code-pkce-flow), designed for client-side apps with no client secret.
- **Nothing leaves your browser.** Your liked songs data is fetched and processed entirely client-side. No server, no database.
- **Token is cached in sessionStorage** for the duration of the browser session so you don't need to re-auth on refresh.
- **Spotify development mode** limits your app to 25 authorized users. This is a personal tool so that limit won't matter.

## why not just use Spotify?

Spotify doesn't expose this ranking anywhere in the app or desktop client. Liked songs is a flat list with no album-level aggregation.
