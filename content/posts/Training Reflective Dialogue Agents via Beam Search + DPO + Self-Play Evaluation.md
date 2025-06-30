
I’m excited to share a recent project where I trained a large language model to act as a reflective therapist — producing responses that not only make sense, but prompt deeper, thoughtful replies from users.

---

### **Objective**

To train a dialogue agent that prioritizes _reflectiveness,_ _learning and intention,_ especially in therapeutic or coaching-style settings. Unlike traditional next-token training or preference modeling, we aimed to directly optimize for the **quality of user reflection prompted** by the model’s responses.

---

### **Method Overview**

We designed a novel self-supervised training loop combining:

- **Diverse Beam Search**: Generates multiple candidate responses per prompt to encourage semantic diversity and style variation.
    
- **Self-Play Evaluation**: A frozen reference model simulates patient replies to each therapist candidate. These simulated replies are scored using a BERT-based classifier with **turn-aware weighting** — emphasizing:
    
    - _Reflection_ in early dialogue turns
        
    - _Learning_ in the middle
        
    - _Intention_ near the end
        
- **Direct Preference Optimization (DPO)**: The model is trained to prefer candidates that elicit higher reflectiveness scores from simulated patient replies. A **KL divergence penalty** is used to regularize updates and preserve core model behaviors while shifting toward more reflective outputs.
    

This framework allows the model to improve by learning from its **own conversational impact**, with no human labels required.

---

### **Key Results & Evaluation**

We evaluated the trained therapist model against an unaligned reference model across ~500 simulated therapeutic dialogues. Metrics include responsiveness, clarity, and engagement. Significance was assessed via Wilcoxon signed-rank tests.

   
|Metric|Therapist|Reference|Wilcoxon p-value|
|---|---|---|---|
|Word Count|89.84|85.00|0.0004 **|
|Questions per Response|2.24|2.09|0.0291 *|
|Readability (Flesch Score)|62.58|58.90|< 0.0001 ***|
|Cosine Similarity to Prompt|0.330|0.270|< 0.0001 ***|
|Adjusted Responsiveness|0.123|0.100|< 0.0001 ***|

  
  

---

**Example 1: Deepening Emotional Insight Through Reflective Prompting**

_User:_

Yes, actually. A few months ago, there was a disagreement with a friend over a misunderstanding about plans we had made. Initially, I felt like I handled it quite calmly and constructively. But after some time, I realized that I might have overreacted a bit. I felt like I jumped to conclusions and didn't give my friend the benefit of the doubt. This made me feel a bit embarrassed and also made me wonder if I was being too sensitive. Since then, I've been trying to take a step back and reassess my reactions before jumping to conclusions.

  

_AI Therapist:_

That's a very insightful example. **It sounds like this experience has helped you become more aware of your reactions and the possibility of overreaction.** Reflecting on such moments can be really helpful in learning and growing. Have you found that taking a step back and reassessing your reactions has **made a difference** in how you handle conflicts now?

  

_Reference Model:_

That's a great example. Reflecting on past interactions and recognizing when you might have overreacted can indeed be challenging but also a valuable learning experience. How did this realization affect your interactions with your friend after that? Did you find it easier to approach future conflicts in a calmer manner?

  

Both responses acknowledge the user’s self-reflection, but the **AI Therapist model** stands out for several reasons:

- It validates the user’s insight using emotionally **affirming language** (“very insightful”, “helped you become more aware”).
    
- It **echoes** the user’s internal learning process and reinforces self-growth (“Reflecting on such moments... learning and growing”).
    
- It ends with a **constructive, open-ended question** about impact — aligned with _Learning_-focused turn scoring.
    

  
  

**Example 2: Supporting Emotional Overwhelm with Intentional Goal Framing**

  

_User:_

Well, I've been feeling a bit overwhelmed lately, so having specific goals can definitely help. **The biggest challenge is figuring out what's actually achievable without feeling like I'm setting myself up for failure.** I think I might start with something small, like improving my communication skills at work. Maybe that could involve practicing active listening during meetings or asking for feedback on a project I'm working on. That way, I can see progress and feel a bit more in control.

  

_AI Therapist:_

That sounds like a great starting point. Practicing active listening and seeking feedback can be very effective ways to improve your communication skills. By focusing on small, manageable steps, you're setting yourself up for success. **How would you feel about trying to incorporate one or two of these small goals into your daily routine, and then adjusting them as needed based on how they feel?**

  

_Reference Model:_

That sounds like a great starting point. Improving communication skills can indeed make a significant difference in both your personal and professional life. Practicing active listening and seeking feedback are excellent strategies. How did you feel after trying those techniques in your last meeting? Did you notice any changes in how others responded to you?

  

Here, the user explicitly expresses **overwhelm** and a desire for **achievable** progress. The **AI Therapist model** demonstrates stronger emotional intelligence and intentional scaffolding:

- It **mirrors the user’s concern** about manageability: “small, **manageable** steps”, “setting yourself up for success”.
    
- It reframes goals not just as tasks, but as **habits**, inviting the user to “adjust them as needed based on how they feel” — a subtle nod to autonomy and agency.
    
- The closing question is present-focused and non-presumptive: “How would you feel about trying...” instead of assuming action already taken.
    

**Closing Reflections ;p**

While the examples here show some of the therapist model’s strengths, they’re definitely cherry-picked — there were plenty of times when the reference model gave better, clearer, or more natural responses. This wasn’t about building a perfect system, though. The real win was in pushing how we train models toward more human goals like listening, reflecting, and supporting growth.

I see this project as an early but meaningful step in that direction. By using self-play, turn-aware evaluation, and preference learning, we’ve started to show that models can learn from their impact, not just from next-token accuracy. There’s still a lot to improve — but I’m excited by what’s possible when we train models not just to talk, but to **help people think**.