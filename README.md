# 🍬 Mochi's Candy Adventure

A browser platformer for one or two players. Run through five candy-themed levels, stomp enemies, beat the bosses, collect tokens and spend them in the shop. Play solo, or share a room with a friend and pass control back and forth while you video chat.

**No install, no build step.** Everything is plain HTML, CSS and JavaScript.

## Play

Hosted with GitHub Pages: `https://<your-username>.github.io/<repo-name>/`

To run locally, open `index.html` in a browser. A local web server is recommended for multiplayer: `python3 -m http.server`, then visit `http://localhost:8000`.

## Files

| File | What it is |
| --- | --- |
| `index.html` | Wrapper page: the game on the left, the video-chat pane on the right (resizable, hideable) |
| `peerjs.min.js` | PeerJS library (v1.5.4), included locally so there's no CDN dependency |
| `candyland_powerups.html` | The game itself (single file, no audio) |
| `.nojekyll` | Tells GitHub Pages to serve files as-is |

When you change the game, also bump the `?v=` number on the iframe in `index.html` so browsers fetch the new version instead of a cached one.

## Controls

| Action | Key |
| --- | --- |
| Move / jump | ← → (or A D) / Space or ↑ |
| Pause (syncs for both players) | Esc |
| Shop | S |
| Take control (watching player) | T |
| Restart | R |
| Boosts | 1 Speed, 2 Giant, 3 Invisibility |
| Moves | Spit Z, Thrust X, Backhand C, Two Hands Q, Use Balls B, Oil Slick E, Come Here M, Off Hand F, Just The Tip G, Double Backhand H, Face It I, Lucky Dip L, Dump In A Cup U, Drink Up O |

Mobile has on-screen buttons for movement and moves.

### Dump In A Cup and Drink Up
Drink Up is gated in two steps: it can't be **bought** until Dump In A Cup has been bought, and it can't be **activated** until Dump In A Cup has been used. Neither move appears in Lucky Dip.

## Bosses

| Boss | Appears | Behaviour |
| --- | --- | --- |
| Jawbreaker | Levels 1-3 | Paces its platform and spits candy |
| Gumdrop Gunner | Levels 2+ | Fires a fan of 3 (5 when angry) |
| Licorice Lash | Levels 3+ | Telegraphs, dashes, then is winded and takes double damage |
| Cotton Bomber | Levels 4-5 | Rains sugar puffs down around you |

Stomp bosses from above. A gold ring means a weak spot: double damage.

## Multiplayer

Pick Host or Join on the title screen and share the room code. The player in control runs the game; the other watches live and can press **T** to take over. The shop, tokens, pause state and boss/enemy positions stay in sync. Connection falls back through several paths automatically (PeerJS, then Trystero, then a relay), so if one fails, wait a few seconds or refresh both players.

## Video chat

Built in: no account, no link and no time limit. Start or join a 2-player room in the game, then **both players click "Join video"** in the right-hand pane and allow camera and mic. The guest's browser calls the host's directly (peer-to-peer, via [PeerJS](https://peerjs.com)). Your friend appears large, you appear in the small corner tile.

- Mic / camera buttons, **↻ Reconnect** (if it freezes or drops) and **Leave**. The pane can be resized (drag the divider) or hidden.
- Video needs a 2-player room, not Solo. If the game's room code changes, the video reconnects itself.
- Video is separate from the game connection, so it keeps working however the game connected.
- Camera and mic need **HTTPS** (GitHub Pages is) or `localhost`.
- On very strict networks (some school, work or mobile-carrier networks) a direct connection can fail. Free public relay (TURN) servers are listed in `index.html` (`ICE`) as a fallback, but they are not guaranteed. A paid TURN service can be dropped in there if you need rock-solid video.

## Contributing / hacking

- All game code lives in one `<script>` in `candyland_powerups.html`: levels (`mkLevel`), shop data (`MOVES`, `BOOSTS`, `OUTFITS`), update loop (`update`), drawing, then the multiplayer section.
- Anything the other player must see goes through `broadcastState` / `applyGameState` (continuous state) or `sendMp` / `handleMpMessage` (events).
- Test in two browser windows (host and guest) before pushing.

## License

No license has been chosen yet. Until one is added, all rights are reserved by the author.
