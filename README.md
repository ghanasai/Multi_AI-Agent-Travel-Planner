# 🌍 Multi-Agent AI Travel Planner

The **Multi-Agent AI Travel Planner** is an intelligent system that generates a personalized day-trip itinerary using **LangGraph**, **LangChain**, **OpenAI GPT models**, and **Gradio**. It takes a natural-language travel request, extracts the city and interests, and produces a customized itinerary using a multi-agent workflow.

---

# 🏗️ Architecture Overview

This project follows a **pipeline-based multi-agent architecture**, where each agent is responsible for a specific task. The system is orchestrated using **LangGraph’s StateGraph**, ensuring a clear, deterministic execution flow.

The images below illustrate the difference between **Single Agent** vs **Multi-Agent** systems and how your project implements a multi-agent pipeline.

### 🔹 Single Agent vs Multi-Agent Architecture  
<img width="1355" height="984" alt="Screenshot 2025-12-01 070740" src="https://github.com/user-attachments/assets/abb9793d-9475-4356-8dc8-d185124daa62" />


### 🔹 LangGraph Workflow Diagram  
<img width="214" height="594" alt="Screenshot 2025-12-01 070625" src="https://github.com/user-attachments/assets/11e7298b-2e7f-44b7-8e75-6971e1e190bc" />


---

## 🧱 **How the Architecture Works**

### **1. Input Layer**
The user enters a natural-language travel request such as:  
> “Plan a day trip to Hyderabad. I like history and food.”

This raw text is stored as `state["user_input"]`.

---

### **2. Processing Layer (Agents)**

The system uses three specialized agents:

#### **🟣 City Extraction Agent**
- Reads the full user request.
- Identifies and extracts the *destination city*.
- Updates `state["city"]`.

Example:  
“Plan a day trip to Hyderabad” → **Hyderabad**

---

#### **🟣 Interest Extraction Agent**
- Detects user preferences (food, beaches, history, temples, etc.).
- Converts them into a structured list.
- Updates `state["interests"]`.

Example:  
“I like history and food” → `["history", "food"]`

---

#### **🟣 Itinerary Generation Agent**
- Uses both `city` and `interests` to generate a full day itinerary.
- Produces a bullet-point list of activities.
- Saves the final plan inside `state["itinerary"]`.

---

### **3. Orchestration Layer — LangGraph StateGraph**

LangGraph ensures each agent runs in the correct order:

