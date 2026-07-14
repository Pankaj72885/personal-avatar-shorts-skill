---
name: flow-avatar-motivational-shorts
description: >
  Use this skill whenever the user wants a motivational Shorts video made with their own avatar
  (@me) in Google Flow using Gemini Omni Flash — a colorful, cinematic, direct-to-camera video,
  10-18 seconds, in two beats. Triggers include: "motivational video banao", "avatar video বানাও",
  "Omni Flash prompt দাও", "jay shetty style video", "avatar shorts", "@me দিয়ে ভিডিও",
  "AUTO" (auto-pick topic), or any request for Flow Agent Instructions + Omni Flash prompts +
  Bengali voiceover + music + title/tags/description for a self-avatar motivational Shorts video.
  Distinct from `mindvyne-master-production` (faceless videos) and `bd-viral-quote-engine`
  (quote-card posts). Outputs TWO files: Flow Production Package (Agent Instructions + Settings +
  per-beat dialogue + prompts with music/camera cues) and SEO Metadata — never repeats a topic,
  tracked via persistent memory.
---

# Flow Avatar Motivational Shorts

নিজের avatar (**@me**) দিয়ে, Google Flow Agent + Gemini Omni Flash ব্যবহার করে ১৬-২০ সেকেন্ডের
রঙিন, সিনেমাটিক, direct-to-camera মোটিভেশনাল Shorts বানানোর জন্য সম্পূর্ণ প্রোডাকশন প্যাকেজ —
প্রতিবার নতুন থিম, কপি-পেস্ট রেডি।

## কেন এই নিয়মগুলো আছে

- Omni Flash প্রতি generation-এ সর্বোচ্চ ~১০ সেকেন্ড দেয়, নেটিভ scene-extension নেই। তাই ভিডিওর
  জন্য ২টা আলাদা generation লাগবে, প্রতিটাতে চরিত্র/লোকেশন/props অভিন্ন রাখতে হবে।
- **কনসিস্টেন্সি: Agent Mode Memory + Ultra-Detailed Text Lock** — Reference image পদ্ধতি
  সরানো হয়েছে। এখন দুটো স্তরে consistency: (১) Flow Agent Mode-এর session memory — Beat 2-এ
  এজেন্টকে তার নিজের Beat 1 আউটপুট দেখে হুবহু মিলিয়ে চালিয়ে যেতে বলা হয়; (২) Agent Instructions-এ
  ultra-detailed character+location বর্ণনা যা প্রতিটা generation-এ text anchor হিসেবে কাজ করে।
  বিস্তারিত: `references/production-guide.md` Section 1 ও 5।
- **১৬-২০ সেকেন্ড, ২ বিট, প্রতিটা ভরাট** — Omni Flash প্রতি generation প্রায় পুরো ১০ সেকেন্ড
  ভিডিও তৈরি করে, ডায়লগ কম দিলেও ক্লিপ ছোট হয় না, বাকিটা silence থেকে যায় ও ক্রেডিট নষ্ট হয়। তাই
  এখন প্রতিটা বিটের ডায়লগ হিসাব করে ~১৮-২৪ শব্দে লেখা হয়, যেন পুরো ৮-১০ সেকেন্ড পূরণ হয়।
- **সরাসরি উপদেশ না, গল্প/দৃশ্য দিয়ে** — মানুষ লেকচার শুনতে চায় না। প্রতিটা স্ক্রিপ্ট এখন একটা
  নির্দিষ্ট রিলেটেবল দৃশ্য/মুহূর্ত (পরিবার, প্রেম, বন্ধুত্ব জড়িত) দিয়ে শুরু হয়, তারপর ইনসাইটে পৌঁছায়
  — সরাসরি উপদেশ বলে শুরু করে না (`theme-bank.md`)।
- **সিস্টেমেটিক ক্যামেরা মুভমেন্ট** — বিট ১ বামে arc, বিট ২ সেই শেষ ফ্রেম থেকেই শুরু করে ডানে arc।
  জোড়া লাগানোর পর প্রায় match-cut-এর মতো মসৃণ লাগে।
- প্রম্পট ইংরেজিতে ভালো কাজ করে, দর্শক বাংলাভাষী — তাই dialogue বাংলায়, বাকি শট-বর্ণনা ইংরেজিতে।
- একই থিম/হুক বারবার এলে চ্যানেল রোবোটিক লাগে — তাই persistent anti-repeat মেমোরি বাধ্যতামূলক।
- আগে ঋতু-ভিত্তিক ambient weather SFX (বৃষ্টির শব্দ) ভিউ কমিয়েছিল — তাই এখন আবহাওয়া/পরিবেশ-ভিত্তিক
  SFX বাদ, বরং থিমের ইমোশন অনুযায়ী ইচ্ছাকৃত instrumental music (শুরু ও শেষ দুই বিটেই)।

## ওয়ার্কফ্লো (প্রতিটা রানে এই অর্ডারে চালাও)

### ১. মেমোরি চেক করো
`references/content-log.md` পড়ো — থিম, location mode সাম্প্রতিক ব্যবহার নোট করো।

### ২. থিম বাছো
ব্যবহারকারী টপিক দিলে সেটাই নাও। না দিলে/\"AUTO\" বললে `references/theme-bank.md` থেকে সবচেয়ে কম
ব্যবহৃত ক্যাটাগরি + তার মুড ট্যাগ (Energetic/Soft) বাছো।

### ৩. Avatar, Location profile, ও Wardrobe ঠিক করো
- **চেহারা** (স্থায়ী): মেমোরি/কথোপকথন থেকে জানা না থাকলে জিজ্ঞেস করো।
- **Location profile বাছাই** (Studio/Home/Outdoor থেকে একটা, লগে কম ব্যবহৃতটা)।
- **Wardrobe** (প্রতি রানে নতুন): `references/wardrobe-guide.md` অনুযায়ী।

### ৪. বাংলা স্ক্রিপ্ট লেখো, ২ বিটে ভাগ করো
`references/theme-bank.md`-এর "রিলেটেবল দৃশ্য/হুক" অনুযায়ী — সরাসরি উপদেশ না, একটা নির্দিষ্ট
রিলেটেবল দৃশ্য/মুহূর্ত দিয়ে শুরু করো (পরিবার/প্রেম/বন্ধুত্ব), তারপর ইনসাইটে পৌঁছাও। প্রতিটা বিটে
~১৮-২৪ শব্দ (৮-১০ সেকেন্ড পূরণ করতে, `production-guide.md`-এর হিসাব দেখো — কম দিলে ক্রেডিট নষ্ট
হয়)। বিট ১ = হুক দৃশ্য, বিট ২ = ইনসাইট+ক্লোজিং, প্রাকৃতিক থামার জায়গায় ভাগ করো।

⚠️ **ব্যক্তিগত স্বীকারোক্তি নিষেধ**: স্ক্রিপ্টকে স্পিকারের একান্ত ব্যক্তিগত কনফেশন ("আমার সম্পর্ক
ভাঙার পর...", "আমি মেসেজ ডিলিট করিনি") হিসেবে ফ্রেম করবে না। এর বদলে সাধারণ পর্যবেক্ষণ বা
সবার জীবনের গল্প হিসেবে ("আমরা হয়তো...", "আমাদের জীবনে দেখা যায়...", "একবার ভাবো —") ফ্রেম করো।

### ৫. Agent Instructions ও Settings লেখো
`references/production-guide.md`-এর Section 3 টেমপ্লেট থেকে Character + active Location + wardrobe বসাও। এটাই Flow প্রজেক্টে একবার সেট করলে বহাল থাকে।

### ৬. প্রতিটা বিটের জন্য Omni Flash প্রম্পট লেখো
`references/production-guide.md`-এর ছয়-উপাদান ফ্রেমওয়ার্ক (Section 5) অনুসরণ করো। প্রতিটা প্রম্পট:
- ইংরেজিতে (dialogue বাদে), **`@me`** দিয়ে
- Location+props বর্ণনা হুবহু (word-for-word) দুই বিটেই
- **সিস্টেমেটিক arc ক্যামেরা মুভমেন্ট** — বিট ২ বিট ১-এর ঠিক শেষ ফ্রেম থেকে শুরু
- **Music cue বাধ্যতামূলক দুই বিটেই** (থিমের মুড অনুযায়ী)
- **Consistency Lock Block বাধ্যতামূলক** — বিট ১-এ standard lock, বিট ২-এ Agent Memory instruction সহ lock (`production-guide.md` Section 5, উপাদান ৬)
- শেষে আলাদা লেবেলে বাংলা dialogue লাইন

⚠️ **দুটো বিট অবশ্যই একই Flow Agent session-এ পরপর জেনারেট করো** — নতুন session খুললে memory রিসেট হয় এবং Beat 2-এর Agent Memory instruction কাজ করে না।

### ৭. Title, Tags, Description লেখো
`references/production-guide.md`-এর SEO সেকশন (Section 10) অনুসরণ করো।

### ৮. মেমোরি আপডেট করো
`references/content-log.md`-এ নতুন এন্ট্রি (তারিখ, থিম, হুক-লাইন, Location mode) যোগ করো।

## ইনপুট ফরম্যাট

| ইনপুট উদাহরণ | ব্যাখ্যা |
|---|---|
| `শৃঙ্খলা নিয়ে ভিডিও` | নির্দিষ্ট থিমে ফুল প্যাকেজ |
| `AUTO` | থিম নিজে বাছো |
| `স্টুডিওতে চাই` / `আউটডোরে চাই` | নির্দিষ্ট location profile override |
| `শুধু প্রম্পট দাও` | Flow Production Package (SEO ছাড়া) |

## আউটপুট: ফোল্ডার স্ট্রাকচার ও ফাইল

ওয়ার্কস্পেসের মূল ডিরেক্টরিতে `content` নামের একটি ফোল্ডার তৈরি করো (যদি না থাকে)। এরপর যখনই নতুন কোনো ভিডিও জেনারেট করবে, ওই `content` ফোল্ডারের ভেতরে একটি নতুন সাব-ফোল্ডার তৈরি করবে।

সাব-ফোল্ডারের নামকরণের নিয়ম: `[সিরিয়াল নম্বর]_[তারিখ]_[সময়]_[টপিকের-নাম]` (যেমন: `1_2026-07-12_20-05_tulona`)
- সিরিয়াল নম্বর: `content` ফোল্ডারের ভেতরের আগের ফোল্ডারগুলো চেক করে পরের নম্বরটি বসাবে। প্রথমবার হলে `1` হবে।

এই নতুন সাব-ফোল্ডারের ভেতরে নিচের দুটি ফাইল সেভ করবে:

| ফাইল | নামকরণ | বিষয়বস্তু |
|---|---|---|
| ফাইল ১ | `[topic-slug]_flow_production.txt` | Agent Instructions + Settings + প্রতিটা বিটের বাংলা dialogue, music/camera cue, Consistency Lock Block, ও ইংরেজি Omni Flash prompt |
| ফাইল ২ | `[topic-slug]_seo_metadata.txt` | ৩টা Title ভ্যারিয়েন্ট + Description + Tags |

## রেফারেন্স ফাইল
- `references/production-guide.md` — কনসিস্টেন্সি সিস্টেম (Agent Mode Memory + Text Lock), বিট-ভাঙার হিসাব,
  Agent Instructions টেমপ্লেট, ছয়-উপাদান ফ্রেমওয়ার্ক (arc camera + Consistency Lock Block + music-mood audio),
  Colorful/Cinematic visual guide, রিটেনশন নোট, বাংলা/ইংরেজি বিভাজন, SEO
- `references/wardrobe-guide.md` — ঋতু-অনুযায়ী পোশাক, জাতীয়/ধর্মীয় (হিন্দু) উপলক্ষ ক্যালেন্ডার
- `references/theme-bank.md` — মোটিভেশনাল থিম + music-mood ট্যাগ
- `references/content-log.md` — পার্সিস্টেন্ট অ্যান্টি-রিপিট মেমোরি (থিম + location mode)

## কন্টেন্ট ইন্টেগ্রিটি
বাস্তবসম্মত, honest মোটিভেশনাল বার্তা দাও। AI-জেনারেটেড ভিডিওকে আসল ফুটেজ হিসেবে চালানোর পরামর্শ
দিও না।
