---
name: flow-avatar-motivational-shorts
description: >
  Use this skill whenever the user wants a motivational Shorts video made with their own avatar
  (@me) in Google Flow using Gemini Omni Flash — a colorful, cinematic, direct-to-camera video,
  10-18 seconds, in two beats, using a reference-image ingredient to lock wardrobe/location/
  props. Triggers include: "motivational video banao", "avatar video বানাও", "Omni Flash prompt
  দাও", "jay shetty style video", "avatar shorts", "@me দিয়ে ভিডিও", "reference image বানাও",
  "AUTO" (auto-pick topic), or any request for Flow Agent Instructions + Omni Flash prompts +
  Bengali voiceover + music + title/tags/description for a self-avatar motivational Shorts
  video. Distinct from `mindvyne-master-production` (faceless videos) and `bd-viral-quote-engine`
  (quote-card posts). Outputs TWO files: Flow Production Package (Instructions + Settings +
  reference-image prompt when needed + per-beat dialogue + prompts with music/camera cues) and
  SEO Metadata — never repeats a topic, tracked via persistent memory.
---

# Flow Avatar Motivational Shorts

নিজের avatar (**@me**) দিয়ে, Google Flow Agent + Gemini Omni Flash ব্যবহার করে ১৬-২০ সেকেন্ডের
রঙিন, সিনেমাটিক, direct-to-camera মোটিভেশনাল Shorts বানানোর জন্য সম্পূর্ণ প্রোডাকশন প্যাকেজ —
প্রতিবার নতুন থিম, কপি-পেস্ট রেডি।

## কেন এই নিয়মগুলো আছে

- Omni Flash প্রতি generation-এ সর্বোচ্চ ~১০ সেকেন্ড দেয়, নেটিভ scene-extension নেই। তাই ভিডিওর
  জন্য ২টা আলাদা generation লাগবে, প্রতিটাতে চরিত্র/লোকেশন/props অভিন্ন রাখতে হবে।
- **টেক্সট বর্ণনা হুবহু কপি করেও drift দেখা গেছে** — তাই এখন প্রতিটা Location mode-এর একটা করে
  **Reference Image** (Ingredients-এ @StudioRef/@HomeRef/@OutdoorRef) ব্যবহার হয়, যেটা টেক্সটের
  চেয়ে অনেক বেশি নির্ভরযোগ্যভাবে wardrobe+location+props লক রাখে।
- **১৬-২০ সেকেন্ড, ২ বিট, প্রতিটা ভরাট** — Omni Flash প্রতি generation প্রায় পুরো ১০ সেকেন্ড
  ভিডিও তৈরি করে, ডায়লগ কম দিলেও ক্লিপ ছোট হয় না, বাকিটা silence থেকে যায় ও ক্রেডিট নষ্ট হয়। তাই
  এখন প্রতিটা বিটের ডায়লগ হিসাব করে ~১৮-২৪ শব্দে লেখা হয়, যেন পুরো ৮-১০ সেকেন্ড পূরণ হয়।
- **সরাসরি উপদেশ না, গল্প/দৃশ্য দিয়ে** — মানুষ লেকচার শুনতে চায় না। প্রতিটা স্ক্রিপ্ট এখন একটা
  নির্দিষ্ট রিলেটেবল দৃশ্য/মুহূর্ত (পরিবার, প্রেম, বন্ধুত্ব জড়িত) দিয়ে শুরু হয়, তারপর ইনসাইটে পৌঁছায়
  — সরাসরি উপদেশ বলে শুরু করে না (`theme-bank.md`)।
- **সিস্টেমেটিক ক্যামেরা মুভমেন্ট** — এলোমেলো ভিন্ন ভিন্ন ক্যামেরা বর্ণনার বদলে প্রতিটা ভিডিওতে একই
  হালকা arc/orbit প্যাটার্ন, আর বিট ২ ঠিক যেখানে বিট ১ শেষ হয়েছে (ফ্রেমিং/অ্যাঙ্গেল) সেখান থেকেই শুরু
  হয় — এতে জোড়া লাগানোর পর প্রায় match-cut-এর মতো মসৃণ লাগে।
- প্রম্পট ইংরেজিতে ভালো কাজ করে, দর্শক বাংলাভাষী — তাই dialogue বাংলায়, বাকি শট-বর্ণনা ইংরেজিতে।
- একই থিম/হুক বারবার এলে চ্যানেল রোবোটিক লাগে — তাই persistent anti-repeat মেমোরি বাধ্যতামূলক।
- আগে ঋতু-ভিত্তিক ambient weather SFX (বৃষ্টির শব্দ) ভিউ কমিয়েছিল — তাই এখন আবহাওয়া/পরিবেশ-ভিত্তিক
  SFX বাদ, বরং থিমের ইমোশন অনুযায়ী ইচ্ছাকৃত instrumental music (শুরু ও শেষ দুই বিটেই)।

## ওয়ার্কফ্লো (প্রতিটা রানে এই অর্ডারে চালাও)

### ১. মেমোরি চেক করো
`references/content-log.md` পড়ো — থিম, location mode সাম্প্রতিক ব্যবহার নোট করো।

### ২. থিম বাছো
ব্যবহারকারী টপিক দিলে সেটাই নাও। না দিলে/"AUTO" বললে `references/theme-bank.md` থেকে সবচেয়ে কম
ব্যবহৃত ক্যাটাগরি + তার মুড ট্যাগ (Energetic/Soft) বাছো।

### ৩. Avatar, Location profile, ও Wardrobe ঠিক করো
- **চেহারা** (স্থায়ী): মেমোরি/কথোপকথন থেকে জানা না থাকলে জিজ্ঞেস করো।
- **Location profile বাছাই** (Studio/Home/Outdoor থেকে একটা, লগে কম ব্যবহৃতটা)।
- **Wardrobe** (প্রতি রানে নতুন): `references/wardrobe-guide.md` অনুযায়ী।

### ৪. Reference Image চেক/তৈরি করো
`references/reference-images.md` দেখো — নির্বাচিত mode-এর reference আগে থেকে আছে ও current
ঋতু/wardrobe-এর সাথে মেলে? থাকলে reuse (স্কিপ করো)। না থাকলে/ঋতু বদলেছে হলে,
`references/production-guide.md`-এর reference-image প্রম্পট (in-character natural pose স্টাইলে)
দাও, ব্যবহারকারীকে Ingredients-এ `@StudioRef`/`@HomeRef`/`@OutdoorRef` নামে আপলোড করতে বলো, আর
`reference-images.md` আপডেট করো।

### ৫. বাংলা স্ক্রিপ্ট লেখো, ২ বিটে ভাঙো
`references/theme-bank.md`-এর "রিলেটেবল দৃশ্য/হুক" অনুযায়ী — সরাসরি উপদেশ না, একটা নির্দিষ্ট
রিলেটেবল দৃশ্য/মুহূর্ত দিয়ে শুরু করো (পরিবার/প্রেম/বন্ধুত্ব), তারপর ইনসাইটে পৌঁছাও। প্রতিটা বিটে
~১৮-২৪ শব্দ (৮-১০ সেকেন্ড পূরণ করতে, `production-guide.md`-এর হিসাব দেখো — কম দিলে ক্রেডিট নষ্ট
হয়)। বিট ১ = হুক দৃশ্য, বিট ২ = ইনসাইট+ক্লোজিং, প্রাকৃতিক থামার জায়গায় ভাগ করো।

### ৬. Agent Instructions ও Settings লেখো
`references/production-guide.md`-এর টেমপ্লেট থেকে Location Library + Ingredients + চেহারা +
wardrobe বসাও। একবার প্রজেক্টে সেট করলে repeat লাগবে না।

### ৭. প্রতিটা বিটের জন্য Omni Flash প্রম্পট লেখো
`references/production-guide.md`-এর সাত-উপাদান ফ্রেমওয়ার্ক অনুসরণ করো। প্রতিটা প্রম্পট:
- ইংরেজিতে (dialogue বাদে), **`@me, @[Mode]Ref`** দুটোই + consistency-reinforcement লাইন
- Location+props বর্ণনা হুবহু (word-for-word), দুই বিটেই
- **সিস্টেমেটিক arc ক্যামেরা মুভমেন্ট** — বিট ২ বিট ১-এর ঠিক শেষ ফ্রেম থেকে শুরু হয় (production-guide.md
  ধাপ ৫)
- **Music cue বাধ্যতামূলক দুই বিটেই** (থিমের মুড অনুযায়ী) — শুরুতে swell, বিট ২-এর শেষে climax
  (production-guide.md ধাপ ৫), কোনো weather/ambient SFX না
- শেষে আলাদা লেবেলে বাংলা dialogue লাইন

### ৮. Title, Tags, Description লেখো
`references/production-guide.md`-এর SEO সেকশন অনুসরণ করো।

### ৯. মেমোরি আপডেট করো
`references/content-log.md`-এ নতুন এন্ট্রি (তারিখ, থিম, হুক-লাইন, Location mode) যোগ করো।

## ইনপুট ফরম্যাট

| ইনপুট উদাহরণ | ব্যাখ্যা |
|---|---|
| `শৃঙ্খলা নিয়ে ভিডিও` | নির্দিষ্ট থিমে ফুল প্যাকেজ |
| `AUTO` | থিম নিজে বাছো |
| `স্টুডিওতে চাই` / `আউটডোরে চাই` | নির্দিষ্ট location profile override |
| `reference image রিফ্রেশ করো` | জোর করে নতুন reference image বানাও (ঋতু/লুক বদলালে) |
| `শুধু প্রম্পট দাও` | Flow Production Package (SEO ছাড়া) |

## আউটপুট: ফোল্ডার স্ট্রাকচার ও ফাইল

ওয়ার্কস্পেসের মূল ডিরেক্টরিতে `content` নামের একটি ফোল্ডার তৈরি করো (যদি না থাকে)। এরপর যখনই নতুন কোনো ভিডিও জেনারেট করবে, ওই `content` ফোল্ডারের ভেতরে একটি নতুন সাব-ফোল্ডার তৈরি করবে।

সাব-ফোল্ডারের নামকরণের নিয়ম: `[সিরিয়াল নম্বর]_[তারিখ]_[সময়]_[টপিকের-নাম]` (যেমন: `1_2026-07-12_20-05_tulona`)
- সিরিয়াল নম্বর: `content` ফোল্ডারের ভেতরের আগের ফোল্ডারগুলো চেক করে পরের নম্বরটি বসাবে। প্রথমবার হলে `1` হবে।

এই নতুন সাব-ফোল্ডারের ভেতরে নিচের দুটি ফাইল সেভ করবে:

| ফাইল | নামকরণ | বিষয়বস্তু |
|---|---|---|
| ফাইল ১ | `[topic-slug]_flow_production.txt` | Agent Instructions + Settings + (দরকার হলে) reference-image প্রম্পট + প্রতিটা বিটের বাংলা dialogue, music/camera cue, ও ইংরেজি Omni Flash prompt |
| ফাইল ২ | `[topic-slug]_seo_metadata.txt` | ৩টা Title ভ্যারিয়েন্ট + Description + Tags |

## রেফারেন্স ফাইল
- `references/production-guide.md` — কনসিস্টেন্সি ও Reference Image সিস্টেম, বিট-ভাঙার হিসাব,
  Agent Instructions টেমপ্লেট, সাত-উপাদান ফ্রেমওয়ার্ক (arc camera scheme + music-mood audio),
  Colorful/Cinematic visual guide, রিটেনশন নোট, বাংলা/ইংরেজি বিভাজন, SEO
- `references/wardrobe-guide.md` — ঋতু-অনুযায়ী পোশাক, জাতীয়/ধর্মীয় (হিন্দু) উপলক্ষ ক্যালেন্ডার
- `references/reference-images.md` — প্রতিটা Location mode-এর reference image freshness ট্র্যাকিং
- `references/theme-bank.md` — মোটিভেশনাল থিম + music-mood ট্যাগ
- `references/content-log.md` — পার্সিস্টেন্ট অ্যান্টি-রিপিট মেমোরি (থিম + location mode)

## কন্টেন্ট ইন্টেগ্রিটি
বাস্তবসম্মত, honest মোটিভেশনাল বার্তা দাও। AI-জেনারেটেড ভিডিওকে আসল ফুটেজ হিসেবে চালানোর পরামর্শ
দিও না।
