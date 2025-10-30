# Form in Drawer – Vue Project

## 🧩 Overview

This project is a **Vue-based form interface** displayed inside a sliding drawer. The main goal was to explore how far one can go using **native HTML and CSS capabilities** — minimizing JavaScript usage while still achieving smooth user interactions and a solid component architecture.

Live version: https://aymenbrahim.github.io/vue-form/

---

## 🎯 Objectives

- Use **as little JavaScript as possible**, relying on **intrinsic HTML validation** and **CSS transitions**.
- Focus on **smooth animations** and **intuitive motion design** using `transition` and `transform`.
- Build with **production-level structure** in mind — reusable components, higher-order components (HOCs), and clear folder hierarchy.
- Make the design **maintainable** using **CSS variables** for consistent theming.

---

## 🎨 Key Features

- **Form inside a Drawer:** A responsive, sliding drawer that displays the form.
- **Native Form Validation:** Leverages built-in HTML validation attributes (`required`, `pattern`, etc.) without external libraries.
- **Smooth Animations:** Implemented entirely with CSS transitions.
- **Reusable Components:** Components are modular and easily extendable.
- **Theming via CSS Variables:** Colors, spacing, and transitions are defined through CSS custom properties.

---

## 🏗️ Architecture

- **Vue 3 + `<script setup>` syntax**
- **Minimal JavaScript**
- **Reusable component structure**
- **Scoped CSS using variables**
- **Transition-based animations**

---

## 🚧 Limitations

Time constraints prevented the completion of:

- **Full accessibility support** (keyboard navigation, ARIA roles refinement)
- **Minor design polish** and responsiveness

---

## 💡 Lessons Learned

This project reinforced the idea that:

- **CSS and HTML alone** can handle most UI behavior elegantly.
- **Animation and transitions** can greatly enhance user experience without extra JavaScript.
- **Component hierarchy** and **clean structure** matter as much as visual design.

---

## 🧰 Tech Stack

- **Framework:** Vue 3
- **Language:** TypeScript
- **Styling:** CSS Variables + Transitions
- **Build Tool:** Vite

---

## 🚀 Setup & Run

```bash
# Install dependencies
npm install

# Run the dev server
npm run dev

# Build for production
npm run build
```

## 📋 To-Do

- **Refine UI for responsiveness:**
- **Add test for form validation**
