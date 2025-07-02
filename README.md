# Airline Satisfaction Analysis

For viewing my thought process, how I handled/solved the project please access the Google Docs link below:

## 1. Project Introduction
Airline customer satisfaction is a critical performance indicator in the aviation industry. In this project, we examine a dataset comprising over 120,000 survey responses from airline passengers. The airline in question, headquartered in Boston, Massachusetts, reported a historical low in satisfaction rates—falling below 50% for the first time. Each survey includes demographic details, flight-related variables, and evaluations of various service dimensions rated on a 1–5 Likert scale.

## 2. Objective
The objective of this study is to develop a data-driven strategy to improve passenger satisfaction by identifying the key service areas influencing customer sentiment. The findings will be presented in the form of an interactive dashboard, enabling airline leadership to prioritize operational improvements efficiently.

## 3. Methodology

### 3.1 Data Transformation in Power BI
To prepare the data for analysis, the original dataset was imported into Power BI’s Power Query Editor. All columns containing Likert scale responses were selected and unpivoted. This produced a normalized structure with two columns:

- **Attribute:** representing the survey question or service category
- **Value:** representing the passenger’s Likert score (1 to 5)

This structure enabled categorical aggregation and comparison across multiple dimensions such as flight class and service type.

### 3.2 Sentiment Classification and Scoring System
Given the use of a 1–5 Likert scale, sentiment was recoded as follows for interpretability:

- **1–2:** Negative
- **3:** Neutral
- **4–5:** Positive

This classification system enabled the calculation of count-based and percentage-based sentiment metrics. Custom DAX measures were developed for each sentiment group.

### 3.3 Measure Calculations in DAX
Key DAX measures created:

- **Count_Positive**: Number of responses rated 4 or 5
- **Count_Negative**: Number of responses rated 1 or 2
- **Count_Neutral**: Number of responses rated 3 (split into two for visual symmetry across the zero axis)
- **%Positive, %Neutral, %Negative**: Each sentiment's proportion of total responses using DIVIDE() and ALLEXCEPT()
- **Net Promoter Score (NPS)**: Adapted for a 1–5 scale as:
     **NPS = %Positive − %Negative**

To preserve accurate denominator context when filtering by flight class or other attributes, the **ALLEXCEPT()** function was preferred over **ALL()** to ensure context-aware calculations.

### 3.4 Ranking and Visualization
To prioritize the most impactful service areas, each attribute was ranked by its NPS using the **RANKX()** function in descending order. Visualizations were built using diverging stacked bar charts centered at 0%, effectively showing the polarity and intensity of sentiment for each service attribute.

## 4. Analytical Findings

### 4.1 Data Context and Analytical Scope
The provided dashboard investigates the recent drop in customer satisfaction for Maven Airlines, which has reached a historical low below 50%. The analysis is based on over 120,000 passenger responses evaluated on a 1–5 Likert scale. Acknowledging the potential overrepresentation of business class passengers (48% of responses) compared to their actual seat distribution (~20% on typical aircraft), the analysis prudently segments data between Economy/Economy Plus and Business Class to avoid misinterpretation due to sampling bias.
![image](https://github.com/user-attachments/assets/325157b7-1872-4315-8022-72d35387fc40)

### 4.2 Class-Specific Insights: Economy and Economy Plus
The dashboard identifies that **80% of Economy and Economy Plus** class passengers express **neutral or negative sentiments** toward their overall experience. Given that these classes comprise the majority of the airline’s customer base, the implications are substantial. This metric suggests a systemic underperformance in the standard service offering and presents a high-impact opportunity for service redesign.

Moreover, this group shows the **highest dissatisfaction concentration in the 20–35 age group**, as evidenced by the area chart. This demographic tends to be digitally literate, convenience-oriented, and value-sensitive. Their dissatisfaction suggests a misalignment between the airline’s offerings and the expectations of a key growth market.
![image](https://github.com/user-attachments/assets/2413d980-fb5f-44e6-95f5-c1a44929b0b4)

### 4.3 Key Service Drivers of Dissatisfaction
The Likert-derived NPS analysis pinpoints five specific service areas where net sentiment is negative—i.e., more detractors (ratings 1–2) than promoters (ratings 4–5). These are:

1. In-flight Wi-Fi Service
2. Ease of Online Booking
3. Online Boarding Process
4. In-flight Entertainment
5. Food and Drink Quality

These areas are consistent with touchpoints that heavily influence pre-flight and in-flight experience, particularly for digital-native passengers. Each category reflects a potential breakdown in digital UX, perceived value, or execution quality. The inclusion of "Online Booking" and "Online Boarding" as separate but related concerns suggests that the airline’s digital interface may lack responsiveness, clarity, or reliability.

The low NPS of **in-flight Wi-Fi** and **entertainment systems** indicates unmet expectations regarding connectivity and content engagement during flight—a critical factor for business travelers and younger flyers alike. Additionally, persistent negative sentiment around **Food and Drink** implies either poor quality control, inadequate customization, or a gap between cost and perceived value.
![image](https://github.com/user-attachments/assets/10617a7c-df29-4f7d-bea2-43186efc5d2b)


### 4.4 Class-Specific Insights: Business
Despite Business Class typically being associated with high satisfaction levels, the analysis reveals that **31% of respondents in this segment reported either neutral or dissatisfied opinions** of Maven Airlines. This proportion is significant given the premium expectations associated with this travel tier.

Age-based segmentation further indicates that the **peak dissatisfaction is concentrated among passengers aged 25 to 37**, a demographic that likely places high importance on digital convenience, consistency in premium service delivery, and personalization.
![image](https://github.com/user-attachments/assets/f091d1f6-8d96-43a4-b3db-9a14535d0417)

### 4.5 Disatisfaction Drivers: Likert-NPS Analysis
A Net Promoter Score (NPS)-based analysis of the Likert scale responses reveals that **9 service dimensions** recorded a negative NPS among Business Class passengers, meaning the percentage of **detractors (ratings 1–2)** exceeds that of **promoters (ratings 4–5)**.

These are the specific service areas with NPS < 0:
1. In-flight Wi-Fi Service
2. In-flight Entertainment
3. Cleanliness
4. Ease of Online Booking
5. Leg Room Service
6. Online Boarding
7. Food and Drink
8. On-board Service
9. Departure and Arrival Time Convenience

These findings span both digital and in-flight service categories. Importantly, **5 of these areas overlap with the Economy & Economy Plus segment**, indicating widespread service underperformance that transcends cabin class. The remaining four issues—cleanliness, leg room, on-board service, and time convenience—suggest that Business Class passengers have higher service expectations that are not being consistently met.
![image](https://github.com/user-attachments/assets/46482ace-de50-4933-8fe4-9ba0a28e542c)


### 4.6 Key Observations
**a. Overlap in Core Dissatisfaction Drivers**
The presence of shared problem areas such as in-flight Wi-Fi, entertainment, online booking, and food service indicates that these shortcomings are airline-wide systemic issues rather than isolated to any single class. Addressing these could improve satisfaction across all segments.

**b. Premium Service Delivery Gaps**
The additional dissatisfaction with leg room, on-board service, and cleanliness reflects failures in meeting elevated expectations within Business Class. These elements form the core of a premium product and their underperformance implies operational inconsistency or a misalignment between service design and customer expectations.

**c. Disproportionate Digital Expectations**
Issues with ease of online booking and boarding further indicate that Business Class passengers—especially those in the 25–37 age range—expect not only luxury but also seamless digital experiences. The current systems may lack speed, personalization, or intuitiveness expected from a premium service brand.
![image](https://github.com/user-attachments/assets/c622975f-c846-4828-bc32-7b6bf04ccebd)


### 4.7 Unified Strategic Recommendations for Service Recovery
Since the analysis reveals **five key overlapping dissatisfaction drivers** across both Economy/Economy Plus and Business Class—specifically:

1. In-flight Wi-Fi Service
2. In-flight Entertainment
3. Ease of Online Booking
4. Online Boarding
5. Food and Drink

…it is both **strategic and cost-effective** to focus on **shared, system-wide improvements** that elevate the experience for all passengers, while maintaining flexibility to scale or tier service where necessary.

**In-Flight Wi-Fi Service**:
**Problem:**  Passengers across all classes rate in-flight Wi-Fi poorly, likely due to limited speed, high pricing, or unreliable connectivity.

**Recommendation:**

- **Negotiate a performance-based contract with a global Wi-Fi provider** (e.g., Panasonic Avionics, Gogo, or Viasat).
- **Introduce a tiered Wi-Fi pricing model:**
  - Free messaging for all passengers (WhatsApp, iMessage, etc.)
  - Basic browsing included for Business Class; optional upgrade for Economy.
  - Premium bandwidth packages available for purchase across all classes.
- **Communicate realistic expectations pre-flight:** a large portion of dissatisfaction stems from unmet expectations rather than outright failure.

**Rationale:** Improves perceived value in Economy; restores premium positioning in Business, while remaining cost-manageable.

**In-Flight Entertainment (IFE)**
**Problem:** Poor content variety, outdated interface, or non-personalized options contribute to dissatisfaction.

**Recommendation:**

- **Shift to a BYOD** (Bring Your Own Device) streaming model, reducing hardware costs.
- **Curate content based on route and passenger demographics**, using survey data to prioritize top genres.
- **Offer early-access content and language personalization**, particularly for long-haul routes.

**Rationale:** Lowers capital expenditure by avoiding new seatback installations, improves engagement across all segments, and provides Business Class with deeper content access without exclusive infrastructure.

**Online Booking Experience**
**Problem:** Passengers find the booking interface unintuitive or slow, especially on mobile.

**Recommendation:**
- **Redesign the website and app with mobile-first principles**, improving load times and reducing booking steps.
- **Implement autofill, saved traveler profiles, and seamless payment options** (e.g., Apple Pay, Google Pay, regional methods).
- **Introduce dynamic fare bundles with clear comparisons** for Economy vs Business Class benefits.

**Rationale:** A single optimized platform benefits all users while enhancing clarity around fare options and upgrades.

**Online Check-in / Boarding**
**Problem:** Online boarding processes are inconsistent or poorly integrated with airport systems.

**Recommendation:**

- **Invest in integrated digital boarding passes and real-time airport gate information**, ideally via push notifications in the app.
- **Collaborate with major hub airports to enable biometric or priority boarding options**, initially for Business Class but expandable over time.
- **Automate baggage tag printing via kiosks**, reducing queue time for Economy travelers.

**Rationale:** A streamlined boarding process improves operational flow and reduces stress across both classes, while allowing premium features to be gradually layered.

**Food and Drink**
**Problem:** Dissatisfaction relates to perceived quality, lack of personalization, and poor value.

**Recommendation:**

- **Redesign the menu using a base-tier + add-on model**:
  - Provide a **standardized, high-quality meal** in all classes (with improved sourcing and freshness).
  - Allow **pre-order customization online** (vegetarian, high-protein, regional flavors), especially for Business passengers.
- Introduce **limited-time special meals** or **sponsored items** to keep menus dynamic and reduce costs.

**Rationale:** Enhances satisfaction in Economy without inflating cost, while preserving differentiation and choice in Business Class.





