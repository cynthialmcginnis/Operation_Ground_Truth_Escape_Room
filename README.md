# Operation Ground Truth

A browser escape room that reviews the foundations of artificial intelligence. Teams walk a 3D corridor, solve a puzzle at each of six locked blast doors, and earn a timestamped certificate at the exit.

The whole game is one HTML file. There is nothing to install and nothing to build.

**Play it:** `https://cynthialmcginnis.github.io/Operation_Ground_Truth_Escape_Room/`

## The scenario

An experimental AI system at the Joint Facility has locked itself down. The contractors who installed it could not say what it is, what it learned from, or what it decides. The override accepts only operators who can.

Six doors stand between the team and the exit. Each door has a terminal. Each terminal wants an override code.

## How it plays

1. The team enters a team name and member names, then starts the clock.
2. The camera walks to a locked door. The team opens its terminal.
3. The team answers every question on the terminal. The answers build the code.
4. A correct code opens the door and shows a short explanation of each answer.
5. After the sixth door, the game shows a Certificate of Escape.

## The six doors

| Door | Name | Topic | Questions |
| --- | --- | --- | --- |
| 1 | The Three Questions | AI systems you already use | 6 |
| 2 | The Vocabulary Vault | Key terms: AI, machine learning, deep learning, algorithm, training data, model | 8 |
| 3 | The Sorting Bay | Categories of AI systems | 9 |
| 4 | The Archive | A short history of AI | 8 |
| 5 | The Boundary Check | Narrow AI and general AI | 7 |
| 6 | The Technology Deck | AI technologies in use today | 7 |

45 questions in all.

## Rules

- **Clock:** 50:00. It runs into overtime instead of locking the team out.
- **Rejected code:** removes 1:00. The game reports how many answers are correct, not which ones.
- **Incomplete code:** no penalty.
- **Hint:** one per door. The first use removes 1:00.
- **Reload:** progress is saved in the browser. A refresh returns the team to the door they were on.
- **Restart:** the Restart button erases the team's progress after a confirmation.

## The certificate

The final screen is a Certificate of Escape. It shows:

- Team name and member names
- Completion date and time, to the second, in the device's time zone
- Time left, clock used, rejected codes, and hints used
- A certificate ID built from the team, the timestamp, and the scores

Teams press **Print certificate** or take a screen capture. The printed page is black on white with the game interface hidden. The door codes do not appear on the certificate.

## Running a session

- **Group size:** teams of three, one laptop or tablet per team.
- **Time:** allow 60 minutes. That covers the briefing, the 50-minute clock, and certificates.
- **Before class:** open the link on the classroom network and confirm the corridor renders.
- **Reusing a device:** press Restart before the next team plays.

## Host it on GitHub Pages

1. Create a public repository.
2. Upload `index.html` and this `README.md`.
3. Open **Settings**, then **Pages**.
4. Under **Build and deployment**, set the source to **Deploy from a branch**.
5. Choose the `main` branch and the `/ (root)` folder. Save.
6. Wait a minute or two. The site appears at `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`.

You can also open `index.html` straight from a folder on any computer.

## Technical notes

- **One file.** HTML, CSS, and JavaScript all live in `index.html`.
- **3D:** [three.js](https://threejs.org/) r128, loaded from cdnjs. If the network blocks it, or the device has no WebGL, the game still runs with the terminals on a flat background.
- **Fonts:** Chakra Petch, IBM Plex Sans, and IBM Plex Mono from Google Fonts, with system fallbacks.
- **Privacy:** the game collects nothing. Team names and progress stay in the browser's local storage on that device. No data is sent anywhere.
- **Accessibility:** every control works from the keyboard. The game honors the reduced-motion setting and skips the walking animation.
- **Browsers:** current Chrome, Edge, Firefox, and Safari.

## Changing the game

Open `index.html` in a text editor.

- **Clock and penalty:** edit `LIMIT` (seconds on the clock) and `PEN` (seconds lost per rejected code or hint) near the top of the script.
- **Questions:** edit the `ST` array. Each door has a name, an intro, a hint, and a list of items.
- **Answers:** the correct answers are stored as hashes in `HASH`, so they are not readable in the page source. If you change a question's answer, replace its hash. Compute it with this function, where `door` and `item` count from 0 and `value` is the answer's code letter or digit:

```js
function hsh(s){ let x = 5381; for (let i = 0; i < s.length; i++) x = ((x << 5) + x + s.charCodeAt(i)) >>> 0; return x.toString(36); }
hsh('gt|' + door + '|' + item + '|' + value);
```

- **Explanations:** the text shown after each door is stored in `EXPL` as base64-encoded JSON. Decode it, edit it, and encode it again.

The hashing keeps answers out of casual view. It is not security. Do not rely on it for graded work.

## Credits

Created by Cynthia McGinnis.

three.js is released under the MIT License. The fonts are released under the SIL Open Font License.
