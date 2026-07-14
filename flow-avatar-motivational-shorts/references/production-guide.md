# Production Guide — Flow Avatar Motivational Shorts

## সূচি
1. কনসিস্টেন্সি সিস্টেম — Agent Mode Memory + Ultra-Detailed Text Lock
2. স্ক্রিপ্ট রাইটিং নীতি (গল্প/দৃশ্য-চালিত) ও বিট-ভাঙার হিসাব (১৬-২০ সেকেন্ড → ২ ভরাট বিট)
3. Agent Instructions টেমপ্লেট (সম্পূর্ণ — কপি-পেস্ট রেডি)
4. Agent Settings
5. ছয়-উপাদান প্রম্পট ফ্রেমওয়ার্ক (ক্যামেরা স্কিম + Music-mood Audio + Consistency Lock)
6. ভিজ্যুয়াল স্টাইল গাইড — Colorful ও Cinematic
7. রিটেনশন/কমপ্লিশন — কেন ছোট ভালো
8. বাংলা dialogue বনাম ইংরেজি প্রম্পট নিয়ম
9. Scene Builder / স্টিচিং ওয়ার্কফ্লো
10. SEO নিয়ম

> Wardrobe (ঋতু ও উপলক্ষ-অনুযায়ী পোশাক) আলাদা ফাইলে — দেখো `references/wardrobe-guide.md`

---

## ১. কনসিস্টেন্সি সিস্টেম — Agent Mode Memory + Ultra-Detailed Text Lock

### কেন এই পদ্ধতি

Reference image (@StudioRef/@HomeRef/@OutdoorRef) সরানো হয়েছে। নতুন পদ্ধতিতে দুটো স্তরে consistency নিশ্চিত করা হয়:

**স্তর ১ — Agent Mode Memory (সবচেয়ে শক্তিশালী টুল)**
Flow-এর Agent Mode-এ এজেন্ট একই session-এ নিজের আগের generation "দেখতে" ও "মনে রাখতে" পারে।
Beat 2-এর প্রম্পটে স্পষ্টভাবে বলা হয়:
> "Look at the video you just generated for Beat 1. Match every single visual detail — face, skin tone, hairstyle, shirt, background, props, lighting color — exactly. Continue only the camera arc and deliver the new dialogue."

এই নির্দেশটা সরাসরি মডেলকে নিজের আউটপুট থেকে reference নিতে বলে, যা static reference image-এর চেয়ে বেশি কার্যকর।

**স্তর ২ — Ultra-Detailed Text Description (fallback anchor)**
Agent Instructions-এ চরিত্র ও তিনটা location-এর এত বিস্তারিত বর্ণনা থাকবে যে প্রতিটা generation-এ মডেলের কাছে কোনো "interpretation gap" থাকবে না। প্রতিটা বিটের প্রম্পটেও ছয়-স্তরের consistency lock থাকবে।

### দুটো স্তর একসাথে চালানোর নিয়ম
1. **Agent Instructions** — একবার Flow প্রজেক্টে সেট করো (Section 3 দেখো)
2. **Beat 1 প্রম্পট** — সম্পূর্ণ location+character বর্ণনা + consistency lock block
3. **Beat 2 প্রম্পট** — Agent Memory instruction ("Look at Beat 1") + camera continuation + একই lock block
4. **একই session** — দুটো বিট অবশ্যই Flow-এর একই Agent conversation-এ পরপর জেনারেট করো। নতুন session-এ memory রিসেট হয়, তাই Beat 1 ও Beat 2 আলাদা session-এ কখনো দিও না।


---

## ২. স্ক্রিপ্ট রাইটিং নীতি ও বিট-ভাঙার হিসাব

### গল্প/দৃশ্য দিয়ে, সরাসরি উপদেশ না
সরাসরি উপদেশমূলক বাক্য ("শৃঙ্খলা ধরে রাখো") মানুষ স্কিপ করে। `theme-bank.md`-এর "রিলেটেবল
দৃশ্য/হুক" কলাম অনুযায়ী **একটা নির্দিষ্ট, রিলেটেবল মুহূর্ত/দৃশ্য দিয়ে শুরু করো** (পরিবার, প্রেম,
বন্ধুত্ব, বা নির্দিষ্ট কোনো মানুষ জড়িত থাকা ভালো) — তারপর সেই দৃশ্য থেকে ইনসাইটে পৌঁছাও, ইনসাইট
আগেই বলে দিও না। কংক্রিট ডিটেইল রাখো (রুমমেট, ছাদ, রিকশা, চা) — নির্দিষ্টতাই বিশ্বাসযোগ্য করে।

⚠️ **ব্যক্তিগত স্বীকারোক্তি নিষেধ**: স্ক্রিপ্টকে স্পিকারের একান্ত ব্যক্তিগত কনফেশন ("আমার সম্পর্ক
ভাঙার পর...", "আমি মেসেজ ডিলিট করিনি") হিসেবে ফ্রেম করবে না। এর বদলে সাধারণ পর্যবেক্ষণ বা
সবার জীবনের গল্প হিসেবে ("আমরা হয়তো...", "আমাদের জীবনে দেখা যায়...", "একবার ভাবো —") ফ্রেম করো।

### ⚠️ ডায়লগ-দৈর্ঘ্য বনাম ক্লিপ-দৈর্ঘ্য (ক্রেডিট নষ্ট এড়াও)
প্রতিটা Omni Flash generation বাস্তবে **প্রায় পুরো ১০ সেকেন্ড ভিডিও তৈরি করে**, ডায়লগ কম দিলেও
ক্লিপ ছোট হয় না — বাকি সময় avatar চুপচাপ দাঁড়িয়ে থাকে, যেটা ক্রেডিট নষ্ট করে। তাই ডায়লগ এমনভাবে
লেখো যেন প্রতিটা বিটের **প্রায় পুরো ৮-১০ সেকেন্ড** পূরণ হয়:
- বাংলা কথা বলার গতি ~২-২.৫ শব্দ/সেকেন্ড ধরো
- প্রতিটা বিটে **~১৮-২৪টা শব্দ** (৮-১০ সেকেন্ড পূরণ করতে) — এর কম দিলে ক্লিপে dead-air/silence
  থেকে যাবে
- মোট স্ক্রিপ্ট (২ বিট) ≈ ৩৬-৪৮ শব্দ
- নাটকীয় মুহূর্তে ইচ্ছাকৃত ছোট পজ থাকতে পারে, কিন্তু সামগ্রিকভাবে ৮-১০ সেকেন্ড পূরণ করাই লক্ষ্য

### বিট বিভাজন
- **বিট ১ = হুক দৃশ্য** (~৮-১০ সেকেন্ড, ~১৮-২৪ শব্দ) — নির্দিষ্ট রিলেটেবল মুহূর্ত দিয়ে শুরু
- **বিট ২ = ইনসাইট + ক্লোজিং** (~৮-১০ সেকেন্ড, ~১৮-২৪ শব্দ) — দৃশ্য থেকে ইনসাইটে পৌঁছে পাওয়ারফুল
  ক্লোজিং লাইনে শেষ
- প্রাকৃতিক থামার জায়গায় ভাগ করো, মাঝ-বাক্যে কখনো না
- মোট ভিডিও ≈ ১৬-২০ সেকেন্ড (২টা ~৮-১০ সেকেন্ড ভরাট বিট)

---

## ৩. Agent Instructions টেমপ্লেট

একবার Flow-এর "Agent Instructions"-এ এই পুরো ব্লকটা বসাও — প্রজেক্ট-লেভেলে বহাল থাকবে।
Wardrobe ও active location mode প্রতি রানে আপডেট করো।

```
=== CHARACTER (LOCKED — DO NOT DEVIATE) ===
Subject: @me — Bengali male, approximately early-to-mid 30s, medium build.
- Face: warm medium-brown skin tone, clean-cut short dark black hair (close-cropped sides, slightly longer on top, no part), calm and naturally expressive.
- Build: medium frame, upright posture when seated or standing.
- Voice: calm, clear, warm Bengali male voice — direct-to-camera delivery.
- Wearing: [আজকের wardrobe — wardrobe-guide.md থেকে নির্দিষ্ট বর্ণনা বসাও]
These character details are FIXED across every single generation in this session. Do not alter face shape, skin tone, hair length/style/color, or build.

=== ACTIVE LOCATION MODE: [Studio / Home / Outdoor — একটা বাছো] ===

[Studio — যদি Studio হয়]:
Location: a modern podcast-style studio corner.
- Foreground: the subject seated at a clean dark desk.
- Microphone: a professional condenser microphone on a boom arm, positioned just outside frame on the subject's left side. A small label on the mic body reads one short thematic English word (e.g. "Focus", "Rise", "Growth") — this label word must remain identical across both beats.
- Background (softly blurred): neutral dark acoustic-panel wall, soft colorful LED accent lights (teal/purple or warm amber — pick one color scheme and keep it FIXED across both beats), one small potted plant on the desk edge.
- Lighting: warm-white key light from slightly above-left on the subject, colored LED fill from behind creating cinematic depth.

[Home — যদি Home হয়]:
Location: a cozy home living-room corner.
- Foreground: the subject seated in a comfortable mid-tone fabric armchair.
- Left side: a warm wooden bookshelf, softly blurred, with a consistent arrangement of books (do not change book positions or colors between beats).
- Right side: a small wooden side table with exactly one ceramic coffee mug and one open notebook — same position both beats.
- Background: soft textured off-white curtains, slightly visible.
- Lighting: warm amber lamp light from the right side creating soft directional glow and gentle shadow depth.

[Outdoor — যদি Outdoor হয়]:
Location: a green public park.
- Background (softly blurred): natural green trees and foliage, a paved walking path partially visible.
- Seating: subject seated on a wooden park bench or standing near it.
- Time of day: natural soft daylight (overcast or golden-hour — pick one and keep FIXED across both beats; do not mix).
- No artificial props; keep background simple and consistent.

=== CONTENT & VISUAL STYLE ===
Content style: Direct-to-camera motivational short, Jay-Shetty-style calm-confident delivery pacing, visually colorful and cinematic. Vertical 9:16 only.
Visual style: Rich cinematic color grading, warm/cool contrast, saturated natural tones, flattering directional lighting with real depth. No flat or muted lighting.
Camera: systematic subtle arc/orbit — Beat 1 arcs left, Beat 2 continues from that angle arcing back right. See beat prompts for exact framing instructions.
Audio: intentional mood-matched instrumental music — no weather/ambient SFX.

=== AGENT DEFAULT RULE ===
For every generation in this session: use @me, the active location described above, and the character details above. Do not introduce any new objects, change any background element, or alter any wardrobe detail unless the prompt explicitly instructs it.
```

---

## ৪. Agent Settings

| Setting | মান |
|---|---|
| Confirm before generating | Always |
| Aspect ratio | 9:16 (vertical) |
| Model | Gemini Omni Flash (video) |
| Outputs per generation | ১ |

---

## ৫. ছয়-উপাদান প্রম্পট ফ্রেমওয়ার্ক

প্রতিটা বিটের প্রম্পট এই ছয়টি উপাদানে সাজাও। কোনোটাই বাদ দেওয়া যাবে না।

### উপাদান ১ — Shot framing & camera motion (সিস্টেমেটিক arc scheme)

**বিট ১:**
```
Shot: Medium shot, eye-level camera height. Camera starts centered on the subject and arcs
slowly and smoothly to camera-left across the full clip duration — subtle, continuous,
no sudden movement — ending at a slightly-left-angle framing. Maintain medium shot throughout.
```

**বিট ২:**
```
Shot: Continuing directly from the previous clip's ending frame — camera starts at the
slightly-left-angle position where Beat 1 ended, matching that exact framing, distance,
and angle precisely. Then arcs slowly and smoothly back toward center, settling at a
gently centered-to-right framing by the final closing line. Medium shot throughout.
```

### উপাদান ২ — Style & Lighting

Location-অনুযায়ী **হুবহু একই বাক্য** দুই বিটেই:

**Studio:**
```
Style: Cinematic, colorful, rich color grading — warm-white key light on subject with
[teal-purple / warm amber — একটা বাছো এবং দুই বিটেই এটাই রাখো] LED accent glow in background.
High saturation, warm-cool contrast. Flattering directional light.
Lighting: Warm-white key light from slightly above-left on subject; colored LED accent
from behind creating depth and separation. No flat lighting.
```

**Home:**
```
Style: Cinematic, colorful, rich warm color grading — deep amber tones with cool shadow contrast.
High saturation on lamp light and bookshelf. Flattering directional soft light.
Lighting: Warm amber lamp light from the right side casting gentle directional glow,
creating soft depth and shadow. Cozy, intimate feel.
```

**Outdoor:**
```
Style: Cinematic, colorful, rich natural color grading — vibrant greens in background,
warm/cool daylight contrast on subject. Flattering natural directional light.
Lighting: Soft natural [overcast / golden-hour — একটা বাছো] daylight, slightly directional.
```

### উপাদান ৩ — Location + Props (হুবহু কপি করো দুই বিটেই)

Agent Instructions-এর active location বর্ণনার প্রতিটা ডিটেইল এখানে হুবহু পুনরাবৃত্তি করো — একটি শব্দও বদলাবে না।

### উপাদান ৪ — Action

কে কী করছে এই বিটে — মুখের ভাব, হাতের অবস্থান, lean।

### উপাদান ৫ — Audio/Music (দুই বিটেই বাধ্যতামূলক)

থিমের মুড (`theme-bank.md`) অনুযায়ী:
- **Energetic/upbeat (E)**: `"modern upbeat instrumental, driving percussion, subtle electronic beat, hopeful major-key melody, no vocals"`
- **Soft/emotional/cinematic (S)**: `"soft cinematic instrumental, gentle piano with warm string swells, emotional and reflective, no vocals"`

**বিট ১-এ লেখো:**
`"Audio/Music: [mood description] — enters with a noticeable swell in the first second, settles under the dialogue, then builds to a satisfying climax in the final moment of this beat."`

**বিট ২-এ লেখো:**
`"Audio/Music: [same mood description as Beat 1] — continues from Beat 1 with the same instrumentation, then builds to a satisfying climax and peak in the final moment of the video as the closing line is delivered."`

কোনো আবহাওয়া/পরিবেশ-ভিত্তিক ambient sound যোগ করবে না।

### উপাদান ৬ — Consistency Lock Block (সবচেয়ে গুরুত্বপূর্ণ — প্রতিটা প্রম্পটের শেষে এই পুরো ব্লকটা রাখো)

**বিট ১-এর শেষে:**
```
VISUAL CONSISTENCY LOCK:
Do not change ANYTHING that is not explicitly described in this prompt.
- Face: keep exact same facial structure, skin tone (warm medium-brown), eye shape and color,
  nose, jaw — do not alter proportions, age, or any facial feature.
- Hair: keep exact same short dark black hair — same length, same cut, same texture.
- Outfit: keep exact same shirt — same color, same fabric texture, same collar, same sleeve length.
  Do not introduce patterns, logos, or different garments.
- Location: keep every background element in the exact same position — do not move, add, or
  remove any object, furniture, prop, or plant. Do not change wall color, curtain texture, or
  lighting color.
- Camera height: always eye-level. Never tilt up or down.
The ONLY things that may change in Beat 2 are: camera arc direction, subject's expression/action, and the dialogue. Everything else must be pixel-perfect identical.

No on-screen text.
```

**বিট ২-এর শেষে (Agent Memory instruction অতিরিক্ত যোগ হয়):**
```
VISUAL CONSISTENCY LOCK — AGENT MEMORY INSTRUCTION:
Look at the video you just generated for Beat 1 in this session.
Match every single visual detail from that output exactly:
- The subject's face, skin tone, hairstyle, and build — identical.
- The shirt: same color, same texture, same fit — do not change a single detail.
- The background: every object in the exact same position as Beat 1 — same bookshelf/mic/plant/
  curtain/bench/desk — nothing added, moved, or removed.
- The lighting: same color temperature, same direction, same intensity as Beat 1.
- The color grading: same warmth, same contrast, same saturation as Beat 1.
Do not alter facial proportions, age, eye color, hair length, or any wardrobe detail.
The ONLY differences from Beat 1 are: camera start angle (continuing the arc), subject action/expression, and the new dialogue.

No on-screen text.
```

---

## ৬. ভিজ্যুয়াল স্টাইল গাইড — Colorful ও Cinematic

- **Framing**: medium shot, চোখ-বরাবর camera height
- **Camera movement**: ধাপ ৫-এর systematic arc scheme — বিট ১ বামে arc, বিট ২ সেখান থেকেই শুরু করে ডানে arc
- **Color & lighting**: rich cinematic color grading, warm-cool contrast, higher saturation, flat/মিউটেড লাইটিং এড়াও
- **Background**: নির্বাচিত Location mode অনুযায়ী, Agent Instructions-এ লক করা
- **Delivery**: সরাসরি ক্যামেরার চোখে তাকিয়ে, স্বাভাবিক হাতের gesture, calm-confident টোন
- **Wardrobe**: `references/wardrobe-guide.md` অনুযায়ী, background-এর বিপরীতে রঙ "pop" করা উচিত
- **Props**: নির্বাচিত mode অনুযায়ী Agent Instructions-এ ফিক্সড

---

## ৭. রিটেনশন/কমপ্লিশন — কেন ছোট ভালো

- প্রথম ১-২ সেকেন্ড সবচেয়ে গুরুত্বপূর্ণ — hook বিটে প্রশ্ন/বোল্ড দাবি দিয়ে শুরু করো
- কোনো dead air না
- সম্পূর্ণ, সন্তোষজনক ক্লোজিং লাইনে শেষ করো
- ১৬-২০ সেকেন্ড, দুটো পুরোপুরি ভরাট বিট (dead-air ছাড়া) — completion rate বাড়ায়, ক্রেডিটও নষ্ট হয় না

---

## ৮. বাংলা dialogue বনাম ইংরেজি প্রম্পট

- পুরো শট-বর্ণনা (framing, style, lighting, location, action, audio, text-rendering, consistency lock) — সবসময় ইংরেজিতে।
- শুধু avatar যা মুখে বলবে সেই dialogue — বাংলায়, আলাদা লেবেলে:
  `Dialogue (spoken in Bengali, lip-synced): "[বাংলা লাইন]"`
- Omni Flash-এর বাংলা উচ্চারণ ও lip-sync কোয়ালিটি ব্যবহারকারী নিজে যাচাই করে নিশ্চিত করেছেন যে ভালো।

---

## ৯. Scene Builder / স্টিচিং ওয়ার্কফ্লো

- দুটো বিট **একই Flow Agent session-এ** পরপর জেনারেট করো — নতুন session খুললে Agent-এর memory রিসেট হয়, তখন Beat 2-এর "Look at Beat 1" instruction কাজ করবে না।
- Scene Builder/Storyboard Editor-এ ক্রমানুসারে সাজাও
- Native scene-extension এখনো নেই, তাই stitching-ই পথ; UI জটিল লাগলে CapCut/Premiere/Resolve বিকল্প। Omni Flash-এর music মনমতো না এলে CapCut-এর trending sounds ব্যবহার করা যায়।

---

## ১০. SEO নিয়ম

- **Title**: ৩টা ভ্যারিয়েন্ট, ৬০ ক্যারেক্টারের নিচে, curiosity/emotional hook প্রথমে
- **Description**: প্রথম ১৫০ ক্যারেক্টার hook, তারপর ২-৩ বাক্যে সারমর্ম, শেষে ৫-৮টা হ্যাশট্যাগ
- **Tags**: ১০-১৫টা বাংলা+ইংরেজি মিশ্র কিওয়ার্ড
- **Multi-platform**: YouTube Shorts এ #Shorts যোগ করো; Instagram/Facebook Reels-এ হ্যাশট্যাগ ৫-৬টায় নামাও
