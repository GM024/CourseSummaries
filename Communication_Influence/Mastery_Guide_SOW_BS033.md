# Course Mastery Guide: SOW-BS033 Communication and Influence (Encyclopedia Edition)


This guide is a master-level study resource optimized for the MSc Behavioural Science curriculum. It features deep-dive literature summaries, GitHub-optimized dynamic conceptual models, and verbatim keyword styling.


### 1. Global Topology


**Figure 1**

*Structural Map of Social Influence and Communication Theories*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    A["SOW-BS033:<br/><span style='color:#e63946'><b>Communication & Influence</b></span>"]:::hub --> B["Information & Beliefs"]:::sandbox
    A --> C["Social Norms & Interactions"]:::sandbox
    A --> D["Choice Architecture"]:::sandbox
    A --> E["Systemic vs. Individual"]:::sandbox
    A --> F["Resistance & Inoculation"]:::sandbox

    B --> B1["Mildenberger"]:::sandbox
    B --> B2["Van der Linden"]:::sandbox
    B --> B3["Meijers & Rutjens"]:::sandbox

    C --> C1["Geiger & Swim"]:::sandbox
    C --> C2["Steentjes"]:::sandbox
    C --> C3["Klaperski"]:::sandbox

    D --> D1["Hertwig"]:::sandbox
    D --> D2["Dorresteijn"]:::sandbox
    D --> D3["Shiota"]:::sandbox

    E --> E1["Chater & Loewen"]:::sandbox
    E --> E2["Gonzales-Arcos"]:::sandbox

    F --> F1["Fransen"]:::sandbox
    F --> F2["Basol"]:::sandbox
```


*Note.* This figure provides a comprehensive hierarchical overview of the SOW-BS033 course themes. It illustrates the primary conceptual domains—ranging from information-based belief systems to the social dynamics of interaction, environmental design of choice, and systemic framing. The central hub is the course itself, which branches into the six thematic weeks. Each paper is categorized under its respective theoretical pillar to facilitate rapid identification of the course's diverse psychological perspectives. The use of dynamic node sizing ensures that each category title is perfectly centered and legible across all viewing platforms.


---


### 🟢 Week 1: The Social Construction of Belief


#### Mildenberger & Tingley (2019): Beliefs about Climate Beliefs


**Detailed Abstract**  
This research challenges the traditional <span style="color:#e63946"><b>Information Deficit Model</b></span>—the assumption that providing more scientific facts is the primary route to behavioral change. The authors argue that collective action is often paralyzed not by a lack of knowledge, but by biased <span style="color:#e63946"><b>second-order beliefs</b></span>: our perceptions of what *others* believe. Through six massive surveys in the US and China, the study identifies a systemic <span style="color:#e63946"><b>egocentric bias</b></span>, where individuals' own views anchor their estimates of the collective norm. This leads to a <span style="color:#e63946"><b>pluralistic ignorance effect</b></span>, where a majority incorrectly assumes they are in the minority. This misperception creates a <span style="color:#e63946"><b>spiral of silence</b></span>, where individuals self-censor to avoid social isolation. Crucially, political elites (e.g., congressional staffers) are found to be even more biased than the public, often underestimating constituent support for climate policy by significant margins. This paper fulfill's the objective of outlining how social perceptions shape political reality.


**Figure 2**

*Theoretical Topology of Second-Order Belief Construction*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Second-Order Beliefs</b></span>"]:::hub
    
    S1(["Simulation View"]):::sandbox --- Hub
    S2(["Egocentric Bias"]):::sandbox --- Hub
    S3(["Anchoring & Adjustment"]):::sandbox --- Hub
    S4(["Pluralistic Ignorance"]):::sandbox --- Hub
    
    Hub --> B1["Spiral of Silence"]:::sandbox
    Hub --> B2["Political Inaction"]:::sandbox
```


*Note.* This conceptual model explains the psychological construction of social reality as described by Mildenberger & Tingley. The central Hub (red-bolded) represents the meta-cognitive target. The rounded satellite nodes depict the internal cognitive mechanisms—Simulation (imagining others), Bias (projecting self), and Anchoring (clinging to initial estimates)—that contribute to the state of Pluralistic Ignorance. The final output boxes demonstrate the behavioral consequences: a collective "Spiral of Silence" and subsequent "Political Inaction," where policy-makers fail to act because they misjudge public consensus. The dynamic box architecture prevents text clipping by calculating node dimensions based on the verbatim labels.


**How to remember**  
Think of the **"Social Mirror."** Your <span style="color:#e63946"><b>second-order beliefs</b></span> are just a reflection of your own views (<span style="color:#e63946"><b>egocentric bias</b></span>). You assume everyone sees what you see, which leads to the **"Lonely Majority"**—everyone wants to act, but no one speaks because they think they're alone.


---


### 🔵 Week 2: Interpersonal Communication & Social Norms


#### Geiger & Swim (2016): Climate of Silence


**Detailed Abstract**  
Investigates the "Climate of Silence" where public discussion lags behind private concern. The study identifies <span style="color:#e63946"><b>pluralistic ignorance</b></span> as the key driver, motivated by <span style="color:#e63946"><b>impression management</b></span>. Individuals fear that speaking up will damage their perceived <span style="color:#e63946"><b>warmth</b></span> and **competence**, leading to <span style="color:#e63946"><b>self-silencing</b></span> to protect their social reputation.


**Figure 3**

*Psychological Barriers to Climate Discussion*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Socially Constructed Silence</b></span>"]:::hub
    
    S1(["Impression Management"]):::sandbox --- Hub
    S2(["Warmth vs Competence"]):::sandbox --- Hub
    S3(["Pluralistic Ignorance"]):::sandbox --- Hub
    
    Hub --> B1["Self-silencing"]:::sandbox
```


*Note.* This diagram shows how reputation management concerns (Warmth vs Competence) mediate the relationship between private concern and public silence. The "Hub" is the collective quiet, while the satellites represent the social fears that force an individual into the behavior of "Self-silencing" to avoid being labeled with negative stereotypes. The content-aware node sizing ensures that complex terms like "Impression Management" are fully encapsulated within their borders.


#### Klaperski-van der Wal et al. (2025): The Competent Confronter


**Figure 4**

*Theoretical Tradeoffs in Behavioral Confrontation*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Confronter's Dilemma</b></span>"]:::hub
    
    S1(["Social Sanctioning"]):::sandbox --- Hub
    S2(["Warmth Penalty"]):::sandbox --- Hub
    S3(["Domain Competence"]):::sandbox --- Hub
    
    Hub --> B1["Social Costs"]:::sandbox
```


*Note.* Illustrates the social evaluation dimensions used during interpersonal confrontation. It maps how standing up for values (Competence) creates a risk of being perceived as socially abrasive (Warmth Penalty), leading to measurable "Social Costs."


---


### 🟡 Week 3: Beyond Nagging Nudges


#### Hertwig & Grune-Yanoff (2017): Nudging and Boosting


**Figure 5**

*Taxonomy of Behavioral Policy Interventions*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Decision Science</b></span>"]:::hub
    
    S1(["Dual-Process Theory"]):::sandbox --- Hub
    S2(["Ecological Rationality"]):::sandbox --- Hub
    
    Hub --> B1["Nudging (System 1)"]:::sandbox
    Hub --> B2["Boosting (System 2)"]:::sandbox
```


*Note.* Contrasts environmental steering (Nudges) with cognitive empowerment (Boosts) based on the underlying targeted psychological systems (System 1 vs System 2).


---


### 🟠 Week 4: I-frames, S-frames, and System Change


#### Chater & Loewenstein (2023): The i-frame and the s-frame


**Figure 6**

*Structural Dynamics of Policy Framing*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Policy Framing</b></span>"]:::hub
    
    S1(["Attribution Error"]):::sandbox --- Hub
    S2(["Responsibilization"]):::sandbox --- Hub
    S3(["Crowding Out"]):::sandbox --- Hub
    
    Hub --> B1["Systemic Inaction"]:::sandbox
```


*Note.* This model illustrates the diversionary effect of individual-level framing (<span style="color:#e63946"><b>i-frame</b></span>). It shows how shifting blame onto consumers (<span style="color:#e63946"><b>responsibilization</b></span>) leads to "Systemic Inaction" by "Crowding Out" support for broader systemic changes.


---


### 🔴 Week 5: The Credibility of Science Communication


#### Van der Linden et al. (2015): Gateway Belief Model


**Figure 7**

*The Consensus Domino Effect*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Consensus Gateway</b></span>"]:::hub
    
    S1(["Expert Consensus"]):::sandbox --- Hub
    S2(["Cognitive Consistency"]):::sandbox --- Hub
    
    Hub --> B1["Policy Support"]:::sandbox
```


*Note.* This model maps the "domino effect" of expert consensus messaging. Once the foundational perception of agreement is shifted (Consensus Gateway), the drive for "Cognitive Consistency" updates causal and risk beliefs, sequentially driving "Policy Support."


---


### 🟣 Week 6: Resistance to Persuasion & Inoculation


#### Basol et al. (2020): Good News about Bad News


**Figure 8**

*The Mechanism of Cognitive Immunity*


```mermaid
%%{init: { 'flowchart': { 'useMaxWidth': false, 'htmlLabels': true }, 'theme': 'neutral', 'themeVariables': { 'fontSize': '14px' }}}%%
graph TD
    classDef sandbox padding-left:20px,padding-right:20px,padding-top:10px,padding-bottom:10px,stroke-width:2px;
    classDef hub padding-left:25px,padding-right:25px,padding-top:15px,padding-bottom:15px,stroke-width:3px,font-weight:bold;

    Hub["<span style='color:#e63946'><b>Cognitive Immunity</b></span>"]:::hub
    
    S1(["Active Inoculation"]):::sandbox --- Hub
    S2(["Tactic Spotting"]):::sandbox --- Hub
    S3(["Refutational Pre-emption"]):::sandbox --- Hub
    
    Hub --> B1["Misinfo Resistance"]:::sandbox
```


*Note.* Models the build-up of mental defense. The Immunity Hub is established through "Active Inoculation" (learning by doing) and "Tactic Spotting," creating a measurable resistance to persuasive manipulation.


**How to remember**  
The **"Fire Drill."** You run a fake drill (inoculation) so your brain knows the exits when a real fire (misinformation) starts.
