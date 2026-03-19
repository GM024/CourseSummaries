# Course Mastery Guide: SOW-BS033 Communication and Influence (Encyclopedia Edition)

> **Status:** This summary has been reviewed twice by the author. However, as a person, I may have made mistakes.

This guide is a master-level study resource optimized for the MSc Behavioural Science curriculum. It features deep-dive literature summaries, GitHub-hardened conceptual models, and verbatim keyword styling.


### 1. Global Topology


**Figure 1**

*Structural Map of Social Influence and Communication Theories*


```mermaid
%%{init: { "flowchart": { "padding": 30, "useMaxWidth": false, "htmlLabels": true }, "theme": "neutral", "themeVariables": { "fontSize": "12px", "fontFamily": "sans-serif" }}}%%
graph TD
    classDef hub fill:#f8edeb,stroke:#e63946,stroke-width:3px,font-weight:bold;
    classDef week1 fill:#e9f5f2,stroke:#2a9d8f,stroke-width:2px;
    classDef week2 fill:#eef4f7,stroke:#457b9d,stroke-width:2px;
    classDef week3 fill:#fefae0,stroke:#e9c46a,stroke-width:2px;
    classDef week4 fill:#fff3e0,stroke:#f4a261,stroke-width:2px;
    classDef week5 fill:#fbe9e7,stroke:#e76f51,stroke-width:2px;
    classDef week6 fill:#f3e5f5,stroke:#8338ec,stroke-width:2px;

    A["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SOW-BS033:<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style='color:#e63946'><b>Comms & Influence</b></span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]:::hub --> B(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Information &<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Belief Systems &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week1
    A --> C(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Social Norms &<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Interactions &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week2
    A --> D(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Driving, Nudging,<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; & Boosting &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3
    A --> E(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Systemic vs.<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Individual &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week4
    A --> F(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Resistance &<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Inoculation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week6

    B --> B1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Mildenberger &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week1
    B --> B2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Van der Linden &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week5
    B --> B3(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Meijers & Rutjens &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week5

    C --> C1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Geiger & Swim &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week2
    C --> C2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Steentjes &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week2
    C --> C3(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Klaperski &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week2

    D --> D1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Hertwig &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3
    D --> D2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Dorresteijn &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3
    D --> D3(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Shiota &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3

    E --> E1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Chater & Loewen &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week4
    E --> E2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Gonzales-Arcos &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week4

    F --> F1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fransen &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week6
    F --> F2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Basol &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week6
```


*Note.* This figure provides a comprehensive hierarchical overview of the SOW-BS033 course themes. It illustrates the primary conceptual domains—ranging from information-based belief systems to the social dynamics of interaction, the tripartite approach to behavioral change (Driving, Nudging, Boosting), and systemic framing.


<details>
<summary><b>Diagram Glossary (Figure 1)</b></summary>

*   **Information & Belief Systems:** The study of how individuals acquire, update, and meta-perceive scientific information and collective norms.
*   **Social Norms & Interactions:** The exploration of how interpersonal talk and group-level misperceptions (pluralistic ignorance) shape behavior.
*   **Driving, Nudging, & Boosting:** The three-pillar framework for behavior change interventions, focusing on motivation, environment, and competence.
*   **Systemic vs. Individual:** The critical evaluation of whether behavioral problems should be solved at the level of the person (i-frame) or the system (s-frame).
*   **Resistance & Inoculation:** The study of psychological defense mechanisms against persuasive manipulation and misinformation.
</details>


---


### 🟢 Week 1: The Social Construction of Belief


#### <span style="color:#457b9d">Mildenberger & Tingley (2019): Beliefs about Climate Beliefs</span>


**Detailed Abstract**  
This research challenges the traditional <span style="color:#e63946"><b>Information Deficit Model</b></span>—the assumption that public inaction stems purely from a lack of scientific facts. This model rests on the flawed <span style="color:#e63946"><b>Knowledge-Behaviour Hypothesis</b></span>, which assumes that accurate information automatically translates into behavior. The lecture highlights three critical failures of this hypothesis: (1) <span style="color:#e63946"><b>Motivated Reasoning</b></span> (information is processed in self-serving ways), (2) <span style="color:#e63946"><b>Bounded Rationality</b></span> (inherent cognitive flaws like the endowment effect), and (3) <span style="color:#e63946"><b>Environmental Contingency</b></span> (behavior driven by situational factors rather than knowledge). Mildenberger & Tingley argue that collective action is paralyzed by biased <span style="color:#e63946"><b>second-order beliefs</b></span>: our perceptions of what others believe. Identifying a systemic <span style="color:#e63946"><b>egocentric bias</b></span>, they show how a <span style="color:#e63946"><b>pluralistic ignorance effect</b></span> causes a majority to self-censor in a <span style="color:#e63946"><b>spiral of silence</b></span>. Correcting these meta-perceptions is essential for unlocking policy support.


**Core Definitions**  
*   <span style="color:#e63946">**Second-order beliefs**</span>: Perceptions of the distribution of beliefs within a population.
*   <span style="color:#e63946">**Information Deficit Model**</span>: The assumption that lack of information is the primary driver of skepticism/inaction.
*   <span style="color:#e63946">**Knowledge-Behaviour Hypothesis**</span>: The assumption that information processing is the primary driver of change.
*   <span style="color:#e63946">**Motivated Reasoning**</span>: Processing information to confirm pre-existing goals/beliefs.
*   <span style="color:#e63946">**Egocentric Bias**</span>: Using one's own internal state to estimate others'.
*   <span style="color:#e63946">**Pluralistic Ignorance Effect**</span>: Falsely believing one's views are in the minority.
*   <span style="color:#e63946">**Spiral of Silence**</span>: Withholding views due to fear of isolation.


---


### 🔵 Week 2: Interpersonal Communication & Social Norms


#### <span style="color:#457b9d">Geiger & Swim (2016): Climate of Silence</span>

**Detailed Abstract**  
Investigates the "Climate of Silence" maintained by <span style="color:#e63946"><b>pluralistic ignorance</b></span> and <span style="color:#e63946"><b>impression management</b></span>. Individuals fear damaging their perceived <span style="color:#e63946"><b>warmth</b></span> and **competence**, leading to <span style="color:#e63946"><b>self-silencing</b></span>. This <span style="color:#e63946"><b>socially constructed silence</b></span> can be broken by providing accurate information about group concern.


#### <span style="color:#457b9d">Klaperski-van der Wal et al. (2025): The Competent Confronter</span>


**Detailed Abstract**  
This research examines the <span style="color:#e63946"><b>social costs</b></span> of confronting unsustainable behavior. It addresses the <span style="color:#e63946"><b>confronter's dilemma</b></span>: the tension between change (competence) and harmony (warmth). The study provides the first empirical support for the emergence of **beneficial competence ascriptions** for confronters who remain logical and calm, mitigating social penalties.


---


### 🟡 Week 3: Driving, Nudging, and Boosting


#### The Tripartite Framework of Behavior Change


**Detailed Abstract**  
The lecture introduces a comprehensive three-pillar approach to behavior change: **Driving**, **Nudging**, and **Boosting**. 
1. <span style="color:#e63946"><b>Driving</b></span> (Motivation) uses high-pressure influence, focusing on **Motivation**, goals, values, and social rewards (e.g., Cialdini’s persuasion principles). Research by **Nolan et al. (2008)** shows that while people *think* environmental values drive them, the <span style="color:#e63946"><b>descriptive norm</b></span> ("the neighbors also do") is the strongest motivator. Obstacles to driving include **reactance** and effort.
2. <span style="color:#e63946"><b>Nudging</b></span> (Choice Architecture) uses low-pressure environmental steering. As defined by Thaler & Sunstein, it alters behavior without forbidding options. It leverages System 1 <span style="color:#e63946"><b>cognitive deficiencies</b></span>.
3. <span style="color:#e63946"><b>Boosting</b></span> (Competence) builds lasting <span style="color:#e63946"><b>competences</b></span> by targeting System 2 or sharpening heuristics. It assumes <span style="color:#e63946"><b>ecological rationality</b></span> and respects autonomy.


#### <span style="color:#457b9d">Hertwig & Grune-Yanoff (2017): Nudging and Boosting</span>


**Figure 5**

*Taxonomy of Behavioral Change Approaches*


```mermaid
%%{init: { "flowchart": { "padding": 30, "useMaxWidth": false, "htmlLabels": true }, "theme": "neutral", "themeVariables": { "fontSize": "12px", "fontFamily": "sans-serif" }}}%%
graph TD
    classDef hub fill:#f8edeb,stroke:#e63946,stroke-width:3px,font-weight:bold;
    classDef week3 fill:#fefae0,stroke:#e9c46a,stroke-width:2px;

    Hub["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style='color:#e63946'><b>Behavior Change</b></span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <span style='color:#e63946'><b>Approaches</b></span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]:::hub
    
    S1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Driving: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Motivation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3 --- Hub
    S2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Nudging: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Environment &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3 --- Hub
    S3(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Boosting: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Competence &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3 --- Hub
    
    Hub --> B1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Choice Architecture &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3
    Hub --> B2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Skill Building &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week3
```


<details>
<summary><b>Diagram Glossary (Figure 5)</b></summary>

*   **Driving:** Increasing internal pressure through rewards, goals, and social norms (Motivation).
*   **Nudging:** Steering behavior through the environment (Choice Architecture).
*   **Boosting:** Increasing individual ability to make good choices (Competence).
</details>


#### Challenges in Behavior Change
*   **Repetitive Nudges:** Can impact perceived transparency and autonomy (Wachner et al., 2021).
*   **Enduring Effects:** Behavior often reverts once a nudge is removed.
*   **Spill-over:** Challenges in reaching behaviors in different contexts (e.g., from hospital to home).
*   **Effort:** Boosting requires significant cognitive effort from the individual.


---


### 🟠 Week 4: I-frames, S-frames, and System Change


#### <span style="color:#457b9d">Chater & Loewenstein (2023): The i-frame and the s-frame</span>


**Detailed Abstract**  
This paper provides a critical evaluation of the <span style="color:#e63946"><b>i-frame</b></span> (individual focus) and its dominance in behavioral science. The authors argue that by focusing on small-scale, individual-level interventions (like nudges), researchers accidentally facilitate corporate <span style="color:#e63946"><b>responsibilization</b></span>—the shifting of blame for systemic problems (like climate change or obesity) onto the consumer. This focus on the i-frame triggers a <span style="color:#e63946"><b>crowding out effect</b></span>, where public and political support for more effective <span style="color:#e63946"><b>s-frames</b></span> (systemic changes, such as taxes, regulations, or infrastructure) is diminished. The "Influence Stack" identifies that while i-frame interventions are easier to implement, they are often insufficient and can be actively harmful if they deflect attention from necessary policy changes.


**Core Definitions**  
*   <span style="color:#e63946">**i-frame**</span>: Focuses on individual behavior and choice architecture while keeping the status quo.
*   <span style="color:#e63946">**s-frame**</span>: Focuses on systemic changes, laws, and infrastructure that alter the status quo.
*   <span style="color:#e63946">**Responsibilization**</span>: Shifting the burden of systemic problems onto individual choices.
*   <span style="color:#e63946">**Crowding Out**</span>: When focus on one type of intervention reduces support for another.


**How to remember**  
The **"Leaky Boat."** The i-frame is like handing everyone a small cup to bail out water (individual effort), while the s-frame is actually plugging the hole in the hull (systemic fix). If you only talk about the cups, people forget the hole exists.


---


### 🔴 Week 5: The Credibility of Science Communication


#### <span style="color:#457b9d">Van der Linden et al. (2015): Gateway Belief Model</span>


**Detailed Abstract**  
The <span style="color:#e63946"><b>Gateway Belief Model (GBM)</b></span> posits that perceptions of <span style="color:#e63946"><b>scientific consensus</b></span> act as a critical "gateway" to other key beliefs. In a randomized experiment, the authors show that exposing the public to a simple <span style="color:#e63946"><b>consensus message</b></span> (e.g., "97% of climate scientists agree") significantly increases the perceived scientific agreement. This change then ripples through a causal chain, increasing the belief that climate change is happening, that it is human-caused, and that it is a serious problem. Ultimately, this increase in <span style="color:#e63946"><b>cognitive consistency</b></span> leads to higher public support for climate policy. This approach leverages <span style="color:#e63946"><b>heuristic processing</b></span>, where consensus acts as a mental shortcut for truth.


#### <span style="color:#457b9d">Meijers & Rutjens (2014): Affirming Belief in Progress</span>


**Detailed Abstract**  
Drawing on <span style="color:#e63946"><b>Compensatory Control Theory</b></span>, this research explores how belief in scientific progress affects environmental behavior. When individuals experience a lack of control, they often compensate by affirming belief in external sources of order, such as science. However, this creates a <span style="color:#e63946"><b>hydraulic relationship</b></span>: as belief in scientific progress increases, individual motivation to act pro-environmentally decreases. This is a form of <span style="color:#e63946"><b>moral licensing</b></span> or "delegation," where individuals feel that since science is solving the problem, they no longer need to exert effort.


**Core Definitions**  
*   <span style="color:#e63946">**Consensus Messaging**</span>: Communicating the degree of agreement among experts.
*   <span style="color:#e63946">**Heuristic Processing**</span>: Using mental shortcuts (like expert agreement) to form judgments.
*   <span style="color:#e63946">**Compensatory Control**</span>: Affirming external order to manage feelings of personal chaos.
*   <span style="color:#e63946">**Hydraulic Relationship**</span>: When an increase in one variable (belief in science) causes a decrease in another (individual effort).


**How to remember**  
The **"Magic Shield."** You believe science is building a giant shield to protect the earth, so you decide you don't need to wear your own raincoat anymore.


---


### 🟣 Week 6: Resistance to Persuasion & Inoculation


#### <span style="color:#457b9d">Fransen et al. (2023): Sixty Years Later</span>


**Detailed Abstract**  
This paper revisits <span style="color:#e63946"><b>Inoculation Theory</b></span> and its application to modern social issues. It confirms that <span style="color:#e63946"><b>refutational pre-emption</b></span>—providing a weakened version of a counter-argument along with a refutation—builds strong resistance against subsequent persuasive attacks on <span style="color:#e63946"><b>cultural truisms</b></span>. The study highlights three primary <span style="color:#e63946"><b>resistance strategies</b></span> used by individuals: **Avoidance** (ignoring the message), **Contesting** (arguing against the source), and **Empowerment** (bolstering one's own existing beliefs).


#### <span style="color:#457b9d">Basol et al. (2020): Good News about Bad News</span>


**Detailed Abstract**  
This research demonstrates the power of <span style="color:#e63946"><b>active inoculation</b></span> through a game-based intervention (e.g., "Bad News"). By letting players "step into the shoes" of a fake news producer, they learn the <span style="color:#e63946"><b>manipulation tactics</b></span> (e.g., emotional language, polarization, conspiracy theories). This "pre-bunking" approach builds <span style="color:#e63946"><b>broad-spectrum inoculation</b></span> and **cognitive immunity**, making individuals more resistant to misinformation across various topics, even those not explicitly covered in the game.


**Core Definitions**  
*   <span style="color:#e63946">**Refutational Pre-emption**</span>: Pre-exposing individuals to a threat and providing the tools to defeat it.
*   <span style="color:#e63946">**Active Inoculation**</span>: Learning by doing (e.g., playing a game) to build resistance.
*   <span style="color:#e63946">**Cognitive Immunity**</span>: A mental state where one is resilient against manipulative rhetoric.
*   <span style="color:#e63946">**Manipulation Tactics**</span>: The specific techniques (polarization, trolling) used to spread misinformation.


**How to remember**  
The **"Fire Drill."** You run a fake drill (inoculation) so your brain knows the exits when a real fire (misinformation) starts.


---


### 🏗️ The Influence Stack: A Conceptual Synthesis


**Figure 6**

*The Hierarchical Layers of Behavioral Intervention*


```mermaid
%%{init: { "flowchart": { "padding": 30, "useMaxWidth": false, "htmlLabels": true }, "theme": "neutral", "themeVariables": { "fontSize": "12px", "fontFamily": "sans-serif" }}}%%
graph BT
    classDef layer fill:#f8f9fa,stroke:#333,stroke-width:2px;
    classDef week1 fill:#e9f5f2,stroke:#2a9d8f,stroke-width:2px;
    classDef week2 fill:#eef4f7,stroke:#457b9d,stroke-width:2px;
    classDef week34 fill:#fff3e0,stroke:#f4a261,stroke-width:2px;
    classDef week56 fill:#f3e5f5,stroke:#8338ec,stroke-width:2px;

    L1(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>1. Individual Layer</b> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Facts & Beliefs) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week1
    L2(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>2. Social Layer</b> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Norms & Talk) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week2
    L3(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>3. Architectural Layer</b> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Nudges & Systems) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week34
    L4(["<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <b>4. Resistance Layer</b> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Mental Defenses) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br/>"]):::week56
    
    L1 --> L2
    L2 --> L3
    L3 --> L4
```


<details>
<summary><b>Diagram Glossary (Figure 6)</b></summary>

*   **Individual Layer:** The foundational facts and first-order beliefs (Week 1).
*   **Social Layer:** The meta-perceptions and interpersonal communication (Week 2).
*   **Architectural Layer:** The environment and choice architecture (Week 3 & 4).
*   **Resistance Layer:** The psychological defenses against being influenced (Week 5 & 6).
</details>
