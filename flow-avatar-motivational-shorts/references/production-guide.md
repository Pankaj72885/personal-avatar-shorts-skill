# Production Guide — Flow Avatar Motivational Shorts

## সূচি
1. ক্যারেক্টার, লোকেশন ও Reference Image কনসিস্টেন্সি
2. স্ক্রিপ্ট রাইটিং নীতি (গল্প/দৃশ্য-চালিত) ও বিট-ভাঙার হিসাব (১৬-২০ সেকেন্ড → ২ ভরাট বিট)
3. Agent Instructions টেমপ্লেট
4. Agent Settings
5. সাত-উপাদান প্রম্পট ফ্রেমওয়ার্ক (ক্যামেরা স্কিম + Music-mood Audio সহ)
6. ভিজ্যুয়াল স্টাইল গাইড — Colorful ও Cinematic
7. রিটেনশন/কমপ্লিশন — কেন ছোট ভালো
8. বাংলা dialogue বনাম ইংরেজি প্রম্পট নিয়ম
9. Scene Builder / স্টিচিং ওয়ার্কফ্লো
10. SEO নিয়ম

> Wardrobe (ঋতু ও উপলক্ষ-অনুযায়ী পোশাক) আলাদা ফাইলে — দেখো `references/wardrobe-guide.md`
> Reference image freshness tracking — দেখো `references/reference-images.md`

---

## ১. ক্যারেক্টার, লোকেশন ও Reference Image কনসিস্টেন্সি

@me অ্যাভাটার একা যথেষ্ট না — টেক্সট বর্ণনা যতই হুবহু কপি করা হোক, কয়েক বিট পরে চুল/ব্যাকগ্রাউন্ড/
জ্যাকেট/সরঞ্জামের ছোট ডিটেইল বদলে যেতে দেখা গেছে। তাই এখন **Reference Image** ব্যবহার করা হয় —
টেক্সটের চেয়ে অনেক বেশি নির্ভরযোগ্য ভিজ্যুয়াল anchor।

### তিনটা fixed location mode + Reference Image
- **Studio**, **Home**, **Outdoor** — প্রতিটার একটা fixed বর্ণনা+props (ধাপ ৩ দেখো), আর প্রতিটার
  **একটা করে reference image** যেটা Flow-এর Ingredients-এ `@StudioRef` / `@HomeRef` / `@OutdoorRef`
  নামে থাকে।
- Reference image **প্রতি Location mode-এর জন্য একটা**, প্রতি ভিডিওতে না — একবার বানালে বারবার
  reuse হয়, শুধু ঋতু/wardrobe বড় বদল হলে রিফ্রেশ করা লাগে। ট্র্যাক করো `references/reference-images.md`-এ।

### Reference Image কীভাবে বানাবে ও ব্যবহার করবে
**ধাপ ক — চেক করো**: `references/reference-images.md` দেখো। নির্বাচিত Location mode-এর
reference আগে থেকে আছে ও এখনো current ঋতু/wardrobe-এর সাথে মেলে? থাকলে ধাপ (খ) স্কিপ করো,
সরাসরি @[Mode]Ref reuse করার কথা বলো।

**ধাপ খ — নতুন বানাও** (Nano Banana/Flow-এর ইমেজ মোডে, @me দিয়ে — প্রথমবার বা ঋতু বদলালে):
```
Photorealistic still of @me, wearing [আজকের wardrobe — wardrobe-guide.md থেকে], [নির্বাচিত
Location profile-এর হুবহু বর্ণনা — ধাপ ৩ থেকে]. Sitting/standing in a natural relaxed pose as if
captured mid-conversation — a candid in-character moment, not a posed lookbook shot. Soft
natural expression. Location-appropriate lighting matching the mode. Medium shot, 9:16
portrait, photorealistic. No text, no watermark.
```
জেনারেট হওয়া ছবিটা Flow-এর Ingredients-এ আপলোড করে `@StudioRef`/`@HomeRef`/`@OutdoorRef` নাম
দিতে বলো। `references/reference-images.md`-এ তারিখ+wardrobe নোট আপডেট করো।

**ধাপ গ — ব্যবহার**: প্রতিটা বিটের প্রম্পটে এখন **দুটো** ইনগ্রেডিয়েন্ট রেফারেন্স থাকবে —
`@me, @StudioRef` (বা যেই mode সক্রিয়) — @me চরিত্রের মুখ/voice লকের জন্য, @[Mode]Ref
wardrobe+location+props লকের জন্য।

### Consistency-এর নিয়ম (সবসময় একসাথে)
1. **@me + @[Mode]Ref** — দুটোই প্রতিটা প্রম্পটে।
2. **হুবহু (word-for-word) reuse** — Location+props বর্ণনা প্রতিটা বিটে অক্ষরে-অক্ষরে একই বাক্য।
3. **টেক্সট reinforcement**, প্রতিটা প্রম্পটের শেষে:
   `Keep the exact same face, hairstyle, outfit, location, and props as reference — do not alter
   facial proportions, age, or eye color, and do not introduce new furniture, objects, or
   equipment, and do not change the room. Change only what this prompt explicitly describes.`
4. **একই session** — দুটো বিট Flow-এর একই conversation-এ পরপর জেনারেট করা ভালো।

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

## ৩. Agent Instructions টেমপ্লেট

চেহারা/কণ্ঠ/তিনটা Location+props profile/স্টাইল প্রজেক্ট-লেভেল — একবার Flow-এর "Agent
Instructions"-এ বসালে বহাল থাকে। wardrobe ও কোন mode আজ active তা প্রতি রানে নতুন।

```
Character: @me — [avatar-এর সংক্ষিপ্ত শারীরিক বর্ণনা — মেমোরি থেকে], wearing [আজকের wardrobe —
wardrobe-guide.md থেকে]. Keep identical face, hairstyle, and voice across every generation.

INGREDIENTS: @me (character/voice) + @StudioRef / @HomeRef / @OutdoorRef (location-specific
reference image — locks wardrobe, location, and props for that mode; see
references/reference-images.md for freshness).

LOCATION LIBRARY (fixed profile বর্ণনা, reference image caption-এও এই একই টেক্সট ব্যবহার করো):

[Studio]: a modern podcast-style studio corner, a professional condenser microphone on a boom
arm positioned just outside frame to one side (small brand label reads a short, thematic English word like "Focus" or "Growth" relevant to the topic on the mic body), soft colorful LED accent lighting glowing softly in the blurred background, a neutral
acoustic-panel wall, a small desk with one potted plant.

[Home]: a cozy home living-room corner, sitting in a comfortable armchair beside a warm wood
bookshelf softly blurred behind, a small side table visible with one coffee mug and an open
notebook, warm ambient lamp light, soft textured curtains in the background.

[Outdoor]: outdoors in a green public park, natural greenery and trees softly blurred behind, a
walking path or bench, natural daylight (specific park/time varies video to video for variety —
@OutdoorRef anchors the general outdoor wardrobe/look, not one specific park).

Content style: Direct-to-camera motivational short, Jay-Shetty-style calm-confident delivery
pacing, but visually colorful and cinematic. Vertical 9:16 only.

Visual style: Rich cinematic color grading, warm/cool contrast, saturated natural tones,
flattering directional lighting with real depth.

Camera: systematic subtle arc/orbit movement across both beats — see ধাপ ৫.

Audio: intentional mood-matched instrumental music in every clip — no weather/ambient SFX.

Default behavior: reuse @me, the active @[Mode]Ref, and the Location Library text for every
clip of this video.
```

## ৪. Agent Settings

| Setting | মান |
|---|---|
| Confirm before generating | Always |
| Aspect ratio | 9:16 (vertical) |
| Model | Gemini Omni Flash (video), Nano Banana (reference image) |
| Outputs per generation | ১ |

## ৫. সাত-উপাদান প্রম্পট ফ্রেমওয়ার্ক

1. **Shot framing & camera motion** — নিচের সিস্টেমেটিক arc scheme ব্যবহার করো, প্রতিবার এলোমেলো
   নতুন বর্ণনা না লিখে:
   - **বিট ১**: camera শুরু হয় centered position থেকে, পুরো duration জুড়ে ধীরে subject-এর
     চারপাশে সামান্য arc করে camera-left দিকে সরে যায় (subtle, slow, smooth, no sudden movement),
     বিট শেষ হয় slightly-left-angle framing-এ, medium shot ধরে রেখে।
   - **বিট ২**: ঠিক সেই **slightly-left-angle framing দিয়ে শুরু** — প্রম্পটে লেখো: "Continuing
     directly from the previous clip's ending frame: camera positioned at a slight left angle to
     the subject, matching the exact framing, distance, and angle where the last clip ended."
     তারপর ধীরে আবার center-এর দিকে বা আরেকটু ডানে arc করে সরে যায়, ক্লোজিং লাইনে থামে।
   - এই ধারাবাহিকতা জোড়া লাগানোর পর প্রায় match-cut-এর মতো মসৃণ লাগবে।
2. **Style** — cinematic, colorful, rich color grading (ধাপ ৬)
3. **Lighting** — dramatic কিন্তু flattering, নির্দিষ্ট করে বলা
4. **Location + props + Ingredients** — `@me, @[Mode]Ref` + Location Library-এর বর্ণনা হুবহু
5. **Action** — কে কী করছে
6. **Audio/Music** — দুই বিটেই বাধ্যতামূলক (শুরু ও শেষ), আর এখন **dynamic swell** সহ — সমান
   ভলিউমে সমান্তরাল না, শুরুতে আর শেষে জোর দাও:
   - থিমের মুড (`theme-bank.md`) অনুযায়ী:
     - **Energetic/upbeat**: "modern upbeat instrumental, driving percussion, subtle electronic
       beat, hopeful major-key melody, no vocals"
     - **Soft/emotional/cinematic**: "soft cinematic instrumental, gentle piano with warm string
       swells, emotional and reflective, no vocals"
   - **বিট ১**: music সামান্য জোরে শুরু হয় (attention-grabbing intro swell প্রথম ১ সেকেন্ডে), তারপর
     dialogue-এর নিচে নেমে আসে (ঢেকে না দিয়ে)
   - **বিট ২**: একই instrumentation ধরে রাখো, কিন্তু ক্লোজিং লাইনের শেষ মুহূর্তে music **climax/peak**
     করে — ভলিউম ও ইন্টেনসিটি বাড়ে, একটা সন্তোষজনক চূড়ান্ত মুহূর্ত তৈরি করে, তারপর ক্লিন কাট
   - প্রম্পটে লিখো: "Audio/Music: [mood description] — enters with a noticeable swell in the
     first second, settles under the dialogue, then builds to a satisfying climax in the final
     moment of [বিট ১-এ: this beat / বিট ২-এ: the video]."
   - কোনো আবহাওয়া/পরিবেশ-ভিত্তিক ambient effect যোগ করবে না
7. **Text rendering** — না চাইলে "No on-screen text" স্পষ্ট করে লিখো

Location, Ingredients, ক্যামেরা-continuity, আর Audio/Music-এর লাইন **কখনো বাদ দেওয়া যাবে না**।

## ৬. ভিজ্যুয়াল স্টাইল গাইড — Colorful ও Cinematic

- **Framing**: medium shot, চোখ-বরাবর camera height
- **Camera movement**: ধাপ ৫-এর systematic arc scheme — এলোমেলো ভিন্ন বর্ণনা না, প্রতিটা ভিডিওতে
  একই প্যাটার্ন পুনরাবৃত্তি
- **Color & lighting**: rich cinematic color grading, warm-cool contrast, higher saturation,
  flat/মিউটেড লাইটিং এড়াও
- **Background**: নির্বাচিত Location mode অনুযায়ী, @[Mode]Ref দিয়ে লক করা
- **Delivery**: সরাসরি ক্যামেরার চোখে তাকিয়ে, স্বাভাবিক হাতের gesture, calm-confident টোন
- **Wardrobe**: `references/wardrobe-guide.md` অনুযায়ী, background-এর বিপরীতে রঙ "pop" করা উচিত
- **Props**: নির্বাচিত mode অনুযায়ী ফিক্সড, @[Mode]Ref দিয়ে locked

## ৭. রিটেনশন/কমপ্লিশন — কেন ছোট ভালো

- প্রথম ১-২ সেকেন্ড সবচেয়ে গুরুত্বপূর্ণ — hook বিটে প্রশ্ন/বোল্ড দাবি দিয়ে শুরু করো
- কোনো dead air না
- সম্পূর্ণ, সন্তোষজনক ক্লোজিং লাইনে শেষ করো
- ১৬-২০ সেকেন্ড, দুটো পুরোপুরি ভরাট বিট (dead-air ছাড়া) — completion rate বাড়ায়, ক্রেডিটও নষ্ট হয় না

## ৮. বাংলা dialogue বনাম ইংরেজি প্রম্পট

- পুরো শট-বর্ণনা (framing, style, lighting, location, action, audio, text-rendering) —
  সবসময় ইংরেজিতে।
- শুধু avatar যা মুখে বলবে সেই dialogue — বাংলায়, আলাদা লেবেলে:
  `Dialogue (spoken in Bengali, lip-synced): "[বাংলা লাইন]"`
- Omni Flash-এর বাংলা উচ্চারণ ও lip-sync কোয়ালিটি ব্যবহারকারী নিজে যাচাই করে নিশ্চিত করেছেন যে
  ভালো — তাই আলাদা সতর্কতা/fallback নোট আর দরকার নেই।

## ৯. Scene Builder / স্টিচিং ওয়ার্কফ্লো

- প্রতিটা বিট আলাদা generation (একই @me + @[Mode]Ref + Location/wardrobe/props/consistency-লাইন)
- Scene Builder/Storyboard Editor-এ ক্রমানুসারে সাজাও
- Native scene-extension এখনো নেই, তাই stitching-ই পথ; UI জটিল লাগলে CapCut/Premiere/Resolve
  বিকল্প। Omni Flash-এর music মনমতো না এলে CapCut-এর trending sounds ব্যবহার করা যায়।

## ১০. SEO নিয়ম

- **Title**: ৩টা ভ্যারিয়েন্ট, ৬০ ক্যারেক্টারের নিচে, curiosity/emotional hook প্রথমে
- **Description**: প্রথম ১৫০ ক্যারেক্টার hook, তারপর ২-৩ বাক্যে সারমর্ম, শেষে ৫-৮টা হ্যাশট্যাগ
- **Tags**: ১০-১৫টা বাংলা+ইংরেজি মিশ্র কিওয়ার্ড
- **Multi-platform**: YouTube Shorts এ #Shorts যোগ করো; Instagram/Facebook Reels-এ হ্যাশট্যাগ
  ৫-৬টায় নামাও
