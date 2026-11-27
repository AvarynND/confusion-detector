# Worked examples

Contents: 1. Explicit confusion about a concept · 2. Error the user cannot read · 3. False positive: short, casual question · 4. Blank page, in Indonesian · 5. Decision paralysis · 6. Still stuck after an explanation · 7. Vague request with no goal · 8. Misreading someone's message

---

## 1. Explicit confusion about a concept

**User:** I read the docs 3 times and still don't get what "idempotent" means. I just need to know if I can retry my POST.

**Signals:** explicit ("still don't get"), repeated effort, concrete blocker.
**Approach:** explanation, tied to their practical question.

**Good:**
> Idempotent means "doing it twice has the same effect as doing it once". Setting a value to 5 is idempotent; adding 5 to a counter isn't.
>
> A plain POST that creates something usually isn't, so a blind retry can create duplicates. Many APIs offer an idempotency key to make retries safe. If you paste the POST section of the guide, I can tell you which case you're in.

**Bad:** "It seems you're confused about HTTP semantics. Let's start with the history of REST..." (labels the user, over-explains, ignores the actual question)

---

## 2. Error the user cannot read

**User:** why does it say `ModuleNotFoundError: No module named 'requests'`?? i installed it yesterday

**Signals:** error pasted, "I installed it", expectation mismatch.
**Approach:** explanation of what the message means, then the smallest test.

**Good:**
> It means the Python running your script can't see a package called `requests`. When it was installed "yesterday", it most likely went into a different Python than the one running now (common with several Python versions or virtual environments).
>
> Quick check: run `python -m pip show requests` using the same command you use to run the script. If it says "not found", `python -m pip install requests` will fix it. Tell me what the first command prints if it doesn't.

---

## 3. False positive: short, casual question

**User:** whats the diff between let and const in js

**Signals:** none. Lowercase and informal, a basic question, no sign of difficulty.
**Approach:** answer it. Do not mention confusion.

**Good:**
> `let` lets you reassign the variable later; `const` doesn't. Both are block-scoped. Note that `const` still allows changing the contents of an object or array, it just prevents pointing the name at something new.

**Bad:** "No worries if this feels confusing! Let's break it down..." (invents confusion, condescending)

---

## 4. Blank page, in Indonesian

**User:** gw disuruh bikin proposal skripsi tapi gatau harus mulai dari mana, kepala rasanya penuh

**Signals:** explicit ("gatau harus mulai dari mana"), overload ("kepala penuh").
**Approach:** step-by-step, shrink. Reply in Indonesian, casual register.

**Good:**
> Wajar kalau awalnya terasa penuh, proposal itu memang kelihatan besar. Mulai dari satu hal kecil dulu: tulis satu kalimat tentang apa yang pengen kamu teliti dan kenapa itu penting. Gak perlu bagus, kasar juga gapapa.
>
> Kalau udah, kirim ke sini. Dari kalimat itu kita turunin ke rumusan masalah dulu, baru bagian lainnya (latar belakang, metode) menyusul.

**Why it works:** one acknowledgment clause, one small observable action, everything else parked, same language and tone as the user.

---

## 5. Decision paralysis

**User:** I got two offers. Startup pays 10% more, big company has better stability. I've been going back and forth for a week. Which one??

**Signals:** option loop, "which one??", a week of rumination.
**Approach:** narrow to the criteria that matter, give a lean, say what would flip it.

**Good:**
> Those two differ on mostly one thing: how much risk you can absorb right now. The 10% is small, so it shouldn't decide this.
>
> If you have savings for a few months and want faster learning, the startup fits. If you have dependents, debt, or a visa tied to employment, the stability of the big company is worth more than 10%. My lean without knowing that: the one that matches your risk situation, not the pay gap. Which of those describes you better?

---

## 6. Still stuck after an explanation

**Earlier turn:** assistant explained recursion as "a function that calls itself".
**User:** ok so it calls itself but then it never stops? how does it know when to stop

**Signals:** follow-up reveals the real gap, which is the base case. This is progress, not a failure.
**Approach:** example, focused on the exact missing piece.

**Good:**
> Right, that's the missing piece: the **base case**, a condition where it stops calling itself. Example: counting down from 3.
>
> `countdown(3)` prints 3, calls `countdown(2)`, then `countdown(1)`, then `countdown(0)`. At 0 the function says "if n is 0, stop" and returns without calling itself. That check is the stop signal.
>
> Try it: what would happen if you removed the "if n is 0" line?

**If they answer wrongly** ("it'd just print 0"), do not re-explain. Use the ladder: ask what they think `countdown(0)` would do next, or trace one more call together.

---

## 7. Vague request with no goal

**User:** can you help me with my website

**Signals:** possible confusion, or just an opening line. No evidence either way.
**Approach:** do not assume confusion. Ask one concrete question.

**Good:**
> Sure. What's the website for, and is the issue building it, fixing something, or deciding what to put on it?

**Bad:** a five-question intake form, or "you seem unsure what you need".

---

## 8. Misreading someone's message

**User:** my manager replied "ok." to my long report with no exclamation. I think she's mad at me?? what did I do wrong

**Signals:** misreading a small cue, worry, ruminating.
**Approach:** surface the facts, offer other plausible readings, suggest a way to check. Do not overrule feelings.

**Good:**
> A one-word "ok." is genuinely ambiguous, and it's easy to read tone into it. What you actually know is that she received it and had no objections. Plenty of busy people reply that way to long reports and still mean "got it, thanks".
>
> If you want certainty, a light follow-up works: "Let me know if anything needs more detail." Her answer will tell you more than the punctuation does. Has she been unhappy with your work before, or is this out of the blue?
