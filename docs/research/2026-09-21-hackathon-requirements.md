# AssemblyAI hackathon requirements and drive-thru fit

Researched on 21 September 2026. This is a requirements brief, not an approved implementation specification. Facts below come from official sources; product recommendations are labeled separately.

## Event-specific facts

- The event runs online, worldwide, from 1–30 September 2026. Registration remains open during the build window.
- Projects must build on AssemblyAI.
- The event page displays the submission deadline as **30 September, 11:00 p.m. Malaysia Time**, equivalent to **15:00 UTC**. The timezone-dependent deadline was verified in the rendered page; the plain-text web extraction omitted it.
- The prize pool is **US$10,000**, split between US$5,000 cash and US$5,000 AssemblyAI credits.
- Personal email addresses are accepted; a company address is encouraged but optional.

Source: [AssemblyAI Voice Agent Hackathon](https://lablab.ai/ai-hackathons/assemblyai-voice-agent-hackathon).

The public event page did not expose a separate detailed rubric, score weights, team-size limit, prize allocation per winner, or specific restrictions on complementary LLM/TTS providers. Those details remain unconfirmed.

## General lablab submission baseline

Every participant must enroll individually and belong to a lablab team, including solo entrants. The general FAQ calls for an online working prototype, video, and pitch deck. [Platform guide](https://lablab.ai/guide)

Prepare these artifacts:

| Artifact | Published guidance |
| --- | --- |
| Project metadata | Title at most 50 characters; summary at most 255 characters; description at least 100 words; category/track and technology tags. |
| Video | At most five minutes, under 300 MB. |
| Demo | Direct URL to the deployed interactive application and its hosting platform. |
| Repository | GitHub URL; identify additional repositories in the main README. |

Source: [Submission walkthrough](https://lablab.ai/ai-articles/hackathon-guidelines).

The rulebook specifies a **public GitHub repository**, **MP4 video**, **PDF slides**, and **PNG/JPG cover at 16:9**. It prohibits plagiarism and cheating. Its general judging dimensions are **Presentation, Business Value, Application of Technology, and Originality**, with each dimension described on a 1–5 scale. [Rulebook](https://lablab.ai/hackathon-rules)

Use those dimensions as preparation guidance; an AssemblyAI-specific weighting was not found.

### Wording differences worth retaining

- The submission guide uses softer wording for public repositories and image proportions; follow the stricter rulebook baseline above. [Submission guide](https://lablab.ai/delivering-your-hackathon-solution)
- The rulebook names Streamlit, Replit, and Vercel; the walkthrough describes hosting more broadly. Resolve this if choosing a different demo platform. [Rulebook](https://lablab.ai/hackathon-rules), [walkthrough](https://lablab.ai/ai-articles/hackathon-guidelines)
- The generic submission guide currently includes an IBM Bob report reference. The AssemblyAI event page does not corroborate it, so it is **not established as a requirement for this event**. [Submission guide](https://lablab.ai/delivering-your-hackathon-solution)
- Aim for a 3–5 minute presentation: the rubric treats a very short presentation unfavorably, but does not establish a separate three-minute eligibility minimum. [Rulebook](https://lablab.ai/hackathon-rules)

No public-source evidence reviewed establishes an AssemblyAI-specific MIT-license mandate or precise policy for pre-existing project code. Recheck the participant-facing submission form and organizer announcements before submitting.

## AssemblyAI capabilities relevant to the concept

AssemblyAI documents two integration approaches: streaming speech recognition with separate LLM, speech synthesis, and orchestration components; or its managed Voice Agent API combining those layers. This brief does not select a stack. [Voice-agent documentation](https://www.assemblyai.com/docs/voice-agents/best-practices)

- **Menu vocabulary:** Keyterm boosting can improve recognition of distinctive product names; it supports up to 100 terms, each at most 50 characters. It does not replace menu validation. [Keyterms](https://www.assemblyai.com/docs/streaming/prompting-and-keyterms)
- **Conversation timing:** Streaming supports turn detection and interruption signals. In a custom stack, playback cancellation and interruption policy still need application handling. [Voice-agent documentation](https://www.assemblyai.com/docs/voice-agents/best-practices)
- **Noisy audio:** Voice Focus documents a far-field variant for settings including drive-thru speakers. Real performance must be evaluated with representative audio. [Voice Focus](https://www.assemblyai.com/docs/streaming/voice-focus)
- **Languages:** English is supported; Malay is absent from the published streaming language table checked here. Avoid promising Malay or English–Malay code-switching until support and performance are verified. [Language documentation](https://www.assemblyai.com/docs/streaming/multilingual-transcription)

These are documentation findings, not tested performance claims. No API requests, credentials, paid services, or runtime experiments were used.

## Drive-thru assessment — recommendations

The team's stated direction is a restaurant drive-thru agent like the ordering experience at McDonald's. My working interpretation is a customer speaks an order, the agent resolves details and corrections, and the restaurant receives an accurate confirmed ticket. A real restaurant partnership, hardware integration, menu, language, and payment workflow have not been specified.

For the hackathon, recommend a browser-accessible drive-thru simulation with a small sample menu, spoken responses, a visible cart, and a simulated kitchen ticket. Give the demonstration a complete ordering outcome:

1. Greet the customer and take multiple items with quantities.
2. Resolve meal size, drink choice, and item-specific modifiers.
3. Handle a correction such as “make that two, and no onions on only one.”
4. Clarify an unavailable or ambiguous item.
5. Read back the order and menu-derived total.
6. Submit the ticket after explicit customer confirmation.
7. Offer staff handoff when the conversation cannot be resolved.

The main engineering risk is preserving correct order state during natural conversation. Menu identifiers, allowed modifiers, availability, prices, and totals should come from structured application data. The language model can interpret requests and propose changes; the application should validate those changes and prevent duplicate submission.

To address originality, choose one demonstrable advantage, such as reliable recovery from corrections under background noise. Present measurable evidence: completed orders, final item/modifier accuracy, correction recovery, and time from end of customer speech to first audible reply. Set targets after a baseline; do not claim reduced restaurant costs or waiting times without evidence.

Keep the first scope focused on one restaurant menu and one verified language. Simulated kitchen delivery, sample prices, and a clear staff-handoff state make the workflow reviewable. Real payments, production POS integration, physical drive-thru hardware, and multi-store operations can be later phases unless the team already has those integrations.

## Current workspace and next decisions

The repository contained only `LICENSE` when inspected; there is no application or technical stack to preserve. This research added only this note.

Before preparing a build specification, settle the demo setting, target language, sample menu, team capacity, and the one differentiator to demonstrate. Then map a small acceptance scenario set to the confirmed submission artifacts and available time.
